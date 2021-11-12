## 10 1 Introduction 

 This paper provides an architectural overview of theAvalancheplatform. The key focus is on the three key differentiators of the platform: the engine, the architectural model, and the governance mechanism. 

 1.1 AvalancheGoals and Principles 

Avalancheis a high-performance, scalable, customizable, and secure blockchain platform. It targets three 15 broad use cases: 

- Building application-specific blockchains, spanning permissioned (private) and permissionless (public)     deployments. 

- Building and launching highly scalable and decentralized applications (Dapps). 

- Building arbitrarily complex digital assets with custom rules, covenants, and riders (smart assets). 

(^1) Forward-looking statements generally relate to future events or our future performance. This includes, but is not limited to,Avalanche’s projected performance; the expected development of its business and projects; execution of its vision and growth strategy; and completion of projects that are currently underway, in development or otherwise under consideration. Forward-looking statements represent our management’s beliefs and assumptions only as of the date of this presentation. These statements are not guarantees of future performance and undue reliance should not be placed on them. Such forward-looking statements necessarily involve known and unknown risks, which may cause actual performance and results in future periods to differ materially from any projections expressed or implied herein.Avalancheundertakes no obligation to update forward-looking statements. Although forward-looking statements are our best prediction at the time they are made, there can be no assurance that they will prove to be accurate, as actual results and future events could differ materially. The reader is cautioned not to place undue reliance on forward-looking statements. 

---

 2 Kevin Sekniqi, Daniel Laine, Stephen Buttolph, and Emin G ̈un Sirer 

20 The overarching aim ofAvalancheis to provide a unifying platform for the creation, transfer, and trade of digital assets. 

 By construction,Avalanchepossesses the following properties: 

Scalable Avalancheis designed to be massively scalable, robust, and efficient. The core consensus engine is able to support a global network of potentially hundreds of millions of internet-connected, low and high25 powered devices that operate seamlessly, with low latencies and very high transactions per second. 

Secure Avalancheis designed to be robust and achieve high security. Classical consensus protocols are designed to withstand up tofattackers, and fail completely when faced with an attacker of sizef+ 1 or larger, and Nakamoto consensus provides no security when 51% of the miners are Byzantine. In contrast, Avalancheprovides a very strong guarantee of safety when the attacker is below a certain threshold, which 30 can be parametrized by the system designer, and it provides graceful degradation when the attacker exceeds this threshold. It can uphold safety (but not liveness) guarantees even when the attacker exceeds 51%. It is the first permissionless system to provide such strong security guarantees. 

DecentralizedAvalancheis designed to provide unprecedented decentralization. This implies a commitment to multiple client implementations and no centralized control of any kind. The ecosystem is designed to avoid 35 divisions between classes of users with different interests. Crucially, there is no distinction between miners, developers, and users. 

 Governable and Democratic $AVAXis a highly inclusive platform, which enables anyone to connect to its network and participate in validation and first-hand in governance. Any token holder can have a vote in selecting key financial parameters and in choosing how the system evolves. 

40 Interoperable and FlexibleAvalancheis designed to be a universal and flexible infrastructure for a multitude of blockchains/assets, where the base$AVAXis used for security and as a unit of account for exchange. The system is intended to support, in a value-neutral fashion, many blockchains to be built on top. The platform is designed from the ground up to make it easy to port existing blockchains onto it, to import balances, to support multiple scripting languages and virtual machines, and to meaningfully support multiple deployment 45 scenarios. 

OutlineThe rest of this paper is broken down into four major sections. Section 2 outlines the details of the engine that powers the platform. Section 3 discusses the architectural model behind the platform, including subnetworks, virtual machines, bootstrapping, membership, and staking. Section 4 explains the governance model that enables dynamic changes to key economic parameters. Finally, in Section 5 explores various 50 peripheral topics of interest, including potential optimizations, post-quantum cryptography, and realistic adversaries. 

---

 AvalanchePlatform 2020/06/30 3 

Naming ConventionThe name of the platform isAvalanche, and is typically referred to as “theAvalanche platform”, and is interchangeable/synonymous with “theAvalanchenetwork”, or – simply –Avalanche. Codebases will be released using three numeric identifiers, labeled “v.[0-9].[0-9].[0-100]”, where the 55 first number identifies major releases, the second number identifies minor releases, and the third number identifies patches. The first public release, codenamedAvalanche Borealis, isv. 1.0.0. The native token of the platform is called “$AVAX”. The family of consensus protocols used by theAvalancheplatform is referred to as the Snow* family. There are three concrete instantiations, called Avalanche, Snowman, and Frosty. 