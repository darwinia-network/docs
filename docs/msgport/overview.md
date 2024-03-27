# Overview

![msgport-overview-1](../images/msgport-overview-1.png)

The Darwinia Msgport encompasses a collection of smart contracts that outline standardized interfaces for facilitating a cross-chain messaging protocol. At the heart of this system is the core interface, [IMessagePort](../msgport/interfaces.md#imessageport), which is designed with flexibility to support various implementations. Notable implementations include [ORMP](../msgport/messaging-protocols/ormp.md), [LCMP](../msgport/messaging-protocols/lcmp.md) and [XCMP](../msgport/messaging-protocols/xcmp.md), each offering distinct characteristics tailored for bridging assets and information to different blockchains.

Applications aiming to integrate with Msgport contracts, or those seeking to comprehend the intricacies of Msgport, should initially consult the [Msgport Workflow documentation](../msgport/workflow.md) and [Tutorials](../msgport/tutorial/remix-demo.md). These resources provide a foundational understanding and step-by-step instructions for a smooth integration process.