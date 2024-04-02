# ORMP

ORMP stands for Oracle Relayer Messaging Protocol. It is an omni-chain messaging protocol that can be used to build decentralized applications, or Dapps, that operate across multiple blockchains with minimal effort for developers. It's named after the two important roles involved in message cross-chaining:

- The Oracle
    
    In this context refers to any source of credible off-chain data. In ORMP, this data refers specifically to the root of an incremental merkle tree composed of cross-chain messages. We refer to this as the `message root` or `msgroot` for short. The message root is used to verify the authenticity of the cross-chain messages. The Oracle can either be a traditional off-chain data service, or a data feed based on the light client. Both of these methods can be used to provide the message root of another chain.
    
- The Relayer
    
    It’s an off-chain piece of software that's responsible for taking messages from one blockchain and relaying them to another. It queries the source chain to find messages that have not yet been relayed, and then relays the message and its proof to the target chain. Once the target chain receives the message, along with the msg_root provided by the Oracle, the target channel can verify the authenticity of the message and process it further if it is found to be valid.
    

These two roles play a vital role in the entire process of sending, verifying, and receiving messages.

## Features

- The cross-chain application provides the option to choose a different Oracle and Relayer if the user does not trust the   ones provided by the official team.
- Messages are stored in an incremental Merkle tree, and the target chain relies on the tree root to validate the legitimacy of the received message.
- The protocol does not guarantee the ordering of messages. However, the application has the option to maintain a nonce or a unique identifier to ensure that messages are received in the correct order, if ordering is necessary. This allows for ordered delivery of messages, even if the protocol itself doesn't provide that guarantee.

## Messaging Design

![msgport-ormp-1](../../images/msgport-ormp-1.png)

### Raw Message Structure

Cross-chain message passing involves wrapping the source data with additional information and transmitting it via a logic channel over the cross-chain network. The accurate structure of the Message to be transmitted is defined as follows:

```solidity linenums="1"
struct Message {
    address channel;     // The messages channel to another chain.
    uint256 index;       // The leaf index lives in channel's incremental mekle tree.
    uint256 fromChainId; // The source chain's chain id.
    address from;        // The application address in the source chain.
    uint256 toChainId;   // The target chain's chain id.
    address to;          // The application address in the target chain.
    uint256 gasLimit;    // The gas limit for destination application used.
    bytes encoded;       // The eth-abi encoded message payload.
}
```

Please be aware that within the channel, all messages are organized in an incremental Merkle tree. The channel is also tasked with receiving and distributing messages, as well as overseeing the management of the message root and its status.

!!! note
    An [incremental Merkle Tree](https://arxiv.org/abs/2105.06009) is a [Merkle Tree](https://en.wikipedia.org/wiki/Merkle_tree) of fixed depth where each leaf start as a zero value, and non-zero values are added by replacing the zero leaves starting from the left-most leaf to the right-most leaf one-by-one.
    **The Incremental Merkle Tree is a gas efficient Merkle Tree.**

### Message Sending Flow

1. The cross-chain application, built on the msgport interface **[IMessagePort](../interfaces.md#imessageport)**, invokes the **`send(from, toChainId, to, gasLimit, encoded_call)`** method of the ORMP. This method is a payable method, meaning it requires the payment of a specific fee to execute. The fee structure is further explained below.
2. Upon receiving the message, the ORMP contracts store it in an Incremental Merkle Tree, emit the `MessageAccepted` event and return msgHash to the sender as the an identifier for that message. 
3. The ORMP contracts then invoke the specified relayer and oracle that have been previously registered with the protocol, emitting the `OracleAssigned` and `RelayerAssigned` event to signal the start of their respective tasks.

Once these two steps are completed, the message sending process is considered finished.

### Message Relaying Flow

The message relaying consists of two crucial roles: the relayer and the oracle service. These components continuously monitor the on-chain ORMP events to determine if there are new tasks assigned to them.

- When the relayer detects a new event, it retrieves the corresponding MessageAccepted event and extracts detailed information about the message from the ORMP contract. It then constructs a message proof using the incremental tree in the corresponding channel of the ORMP. The relayer invokes the `relay(Message calldata message, bytes calldata proof)` method on the relayer contract on the target chain, completing the relay of the message and its proof.
- When the oracle detects a new event, the oracle nodes fetch the corresponding `msg_root` which contains the message. They sign the `msg_root` and send it to a specific multisig contract, which collects all the oracle node signatures. Once the multisig contract gathers enough signatures (typically 3/5), the oracle network triggers the setting of the `msg_root` to the oracle component in the ORMP contracts, completing the relay of the `msg_root`.

For the message to be executed in the ORMP target chain contracts, it requires both the message payload, proof, and a valid oracle `msg_root`.

### Message Receiving Flow

When the `relay` method of the target chain contract is invoked, it performs the following validations:

- Verifies that the sender (relayer) is registered.
- Ensures the proof corresponds with the `msg_root`.
- Confirms that the message's `to` field matches the destination `chainId`.
- Checks whether the message has already been dispatched.

If the validation is successful, the message is then sent to the corresponding user application. Unless an exception occurs, the user contract's method is invoked to complete the cross-chain task associated with the message. At this point, we can consider the cross-chain message to have reached its destination.

##  Cross-chain Fee

The fee for cross-chain messaging is paid in the native token of the source chain. The application can retrieve the cross-chain fee by calling the **`fee`** function in the **[IMessagePort](../interfaces.md#imessageport)** interface.

$$
Fee = OracleFee + RelayingFee
$$


The total cross-chain fee consists of two parts: the oracle fee and the relayer fee. The oracle fee covers the cost of the message root oracle service. The relayer fee includes both the fee for relaying the message and the fee for executing the message on the target chain. If the fee paid exceeds the actual required fee, the excess amount will be refunded to the application.

### OracleFee

The fee for an oracle on a specific chain is determined, see the [fee page](https://github.com/darwinia-network/ORMP/blob/main/script/input/1/fee.c.json#L2).

### RelayerFee

The relayer fee is composed of the execution fee and the payload fee, with various factors influencing the calculation as detailed on the [fee page](https://github.com/darwinia-network/ORMP/blob/main/script/input/1/fee.c.json#L10).

$$
ExecutionFee = dstGasPriceInWei * (baseGas+gasLimit) * dstPriceRatio
$$

$$
PayloadFee = gasPerByte * size * dstGasPriceInWei * dstPriceRatio
$$