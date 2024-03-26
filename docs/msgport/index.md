# Msgport

The [Darwinia Msgport](https://github.com/darwinia-network/darwinia-msgport) is a collection of smart contracts that have been specifically designed to offer a standardized interface for exchanging messages between various blockchains. It eliminates the complexities of different blockchain technologies and facilitates cross-chain interoperability by enabling other smart contracts to send and receive in-chain message calls.

By leveraging these capabilities, cross-chain Dapps built on the Msgport can provide users with an experience that closely resembles that of traditional single-chain Dapps. The Darwinia Msgport opens up a multitude of possibilities for the development of truly multi-chain Dapps.

## Architecture

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a2739a4f-1eb7-4ba9-b2d2-18c34ed5b60d/ce92cb03-4609-44f5-9dc0-d4ff4925941d/Untitled.png)

The Darwinia Msgport is built on a flexible and modular architecture, providing users with the ability to utilize various cross-chain messaging layers that best align with their specific requirements. The Msgport framework offers support for sending arbitrary messages through different low-level cross-chain messaging services. Currently, two protocols are supported: [LCMP](https://www.notion.so/LCMP-Deprecated-d205c8d8e5794c789065aabdbb5f78c8?pvs=21) (Light Client Messaging Protocol) and [ORMP](https://www.notion.so/ORMP-644d05b64d7b4e0d83a7d76bfcbd539b?pvs=21) (Oracle Relayer Messaging Protocol). These protocols provide different capabilities and characteristics, allowing multi-chain application developers to choose the most suitable cross-chain messaging layer for their users. By utilizing in-chain message calls to Msgport contracts, smart contracts can establish communication and interaction across heterogeneous chains. This enables seamless interoperability between different Ethereum Virtual Machine (EVM) compatible blockchain networks.