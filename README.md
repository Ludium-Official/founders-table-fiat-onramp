# [Ludium] zkTLS Builder Escrow Payment Service

# Project Background

![Ludium - Web3 Builder Community.pptx.png](https://i.ibb.co/cKsTwm88/Ludium-Web3-Builder-Community-pptx.png)
The digital native world opens new doors for the great opportunity for the workforce. For one, it is **geographically agnostic** for anyone to work from anywhere. Two, it allows **asynchronous** project management that fosters innovation. And finally, it promotes **pluralistic contribution** where anyone can choose to work for the task that fits them. However, under the current system of work, we are still bounded to work in a place at the designated time for one organization.
Ludium believes that the new world begs for a new system. For this, we develop a system that is **accessible, collaborative and trustless** for the liberty of the builders.

# Project Overview

## Problem

Blockchain and crypto provides an infrastructure for the decentralized global payment. However, there are a few critical bottle necks to bring crypto builder payment solutions to a mass adoption:

1. Fiat Onramp: Crypto is segregated from the conventional payment services (ex. Paypal, Venmo) such that there is no easy way to pay crypto with fiat. It hinders the user experience for onboarding
2. Verifiability: Builder payment requires multiple verification process. Unless information such as KYC, resume, and work completion, can be validated, payment simply cannot happen. For this, however, it usually requires access to the data outside of the onchain records
3. Privacy: At times, there are sensitive information including corporate secrets and builder identity that needs to stay confidential. However, the current public blockchain structure cannot ensure selective disclosure or information

[ZKP2P](https://docs.zkp2p.xyz/) shows that it is possible to integrate full fiat onramp using zkTLS / MPC. However, there is no such solution that uses Mina Protocol as zk prover and verifier

## Solution

Ludium’s zkTLS Builder Escrow Payment service offers

1. **Portal**: Portal is a web app that serves as the frontend for the sponsors to set up the programs and recruit builders to work. Anyone become the sponsor which builds a smart contract that functions as a Escrow Treasury
2. **Escrow Treasury**: Escrow Treasury is the smart contract that settles payment once the proposed work is completed. All works are submitted through the portal and once the validators finalize the work completion, settlement is made
3. **zkTLS Oracle**: zkTLS Oracle is used for the validators to finalize the work completion. Depending on the nature of the work, sources of the data may vary

## Impact

Luduim’s zkTLS Builder Escrow Payment codes will be open sourced for the public use. In the short term, it can have the following usecases

1. **Airdrops / Marketing**: As of now, massive airdrop campaigns are mostly limited to onchain data(eg. NFT holders, LP, Transaction history). With the help of zkTLS, more abundant types of missions and marketing activities can be possible
2. **Hackathons / Contests**: Most hackathon platforms is not integrated with the onchain treasury which makes the payment process painfully slow. With the escrow treasury, it makes the settlement easy and fast
3. **Grant Allocation**: Grant allocation is takes a very long time. Escrow treasury can make it easier for the grant allocators to check the submitted works and make payment fast
4. **Recruitment**: With the a possible exception of superteam earn, no recruitment service provide payment on the platform. Whether it be full time hiring or part time freelancing, HR services can use escrow for the head hunting fees or project completion payment
5. **Investment**: Web3 crowd funding(eg. ICO / IDO) issues token without a way to lock conditions. For instance, pre-TGE investment, eg. points, rely on teams for the distribution after the token issuance. With the help of zkTLS oracle and escrow service, there can be more sophisticated investment contracts

In the longer term, the potential is endless. Just within the scope of the payment, fiat on-off ramp and escrow service can literally be used for everything, let’s say for buying coffee. Everytime anyone make any payment, it will trigger the general zkTLS framework developed through Mina

## Audiences

* **Sponsors**
    * Web3 Foundations: Web3 foundations can directly lock-up their tokens through escrow contract and distribute them. It can be particularly useful for the global grant management and/or other ambassador programs
    * Corporations: Corporations looking to hire talents can set up programs. It can range from freelancer / new project hiring to fulltime hiring referral programs
    * Investors: Investors can lock-up their assets on the escrow contract which will be paid once the condition is met. For instance, they can lock up the full amount which will be distributed initially for the project development, while the rest is paid upon conditions (eg. development, TVL metrics, TGE completion, revenue distribution, etc)
* **Builders**
    * Individual: Individuals looking for freelancer positions can check the programs and complete the required tasks to receive the payment
    * Project Teams: Project teams at different stages can scout for grants and/or investment opportunities. They can even recruit team members through the portal
    * HR Agencies: HR agencies can check the referral programs, recruit suitable teams, and receive payment. They can also become a validator who checks the milestone upon permission from the sponsors

# Architecture

* Portal Overview
    ![image.png](https://i.ibb.co/ZRNr78d0/image.png)
    Portal is the comprehensive escrow system where sponsors, builder and validators interact with one another for the builder payment. It consists of the following functionality:
    * **Set up the program**: Sponsors can enter the portal to set up a program. They can choose to allocate fund by setting up a contract or without a fund. Sponsors can also designate validator(s) who review proposals and milestones
    * **Check Proposal**: Builders can view the program and submit their proposal. It could range from the completed task to planning materials for the future. Once the proposal is submitted, validators view the content and decide whether to proceed with the project with milestones
    * **Submit Milestone**: Once the project page is set up, builders submit their progress on the page to show that they have reached the milestones. Milestones can range from application development to other impact metics depending on the nature of the project. Validators review the submission to see if the milestone is reached.
    * **Settlement**: When a milestone is completed, builders are allocated resources as specified by the project milestone. If the program include the onchain fund under contract, the payment will be settled from the fund. If there is no fund, it will be outside the system
* Sponsor Pay with Fiat
    ![image.png](https://i.ibb.co/TxL1H1mL/image.png)
    One of the most direct usecase for the builder escrow service will be fiat payment that triggers onchain treasury setup. Sponsor sets up the escrow treasury in the following way
    * **Sponsor make fiat payment**: While setting up a program, sponsors can make payment in fiat via PG services (ex. Venmo) whose information creates a unique ID
    * **zkTLS confirms the payment:** Sponsor’s fiat payment is confirmed by triggering zkTLS oracle via ZKON API. Through zkTLS, the information stored on PG services are matched with the uniqueID stored on the backend to verify the amount sent
    * **Escrow treasury is set up:** Once the amount is confirmed, escrow treasury for the program is finally set up. The treasury amount is later to be paid to builders once the work is verfied
* Builder KYC
    ![image.png](https://i.ibb.co/60tnNXr9/image.png)
    The other immediate usecase for builder verification is KYC. Before the payment can be made, KYC is critical to ensure that the builder identity indeed matches with the one to whom the payment is supposed to be made. For the ease of use, our KYC will use [bianceID](https://developers.binance.com/docs/binance-pay/api-order-payer-verification) on Binance Payment Verifier.

\*\* **Note 1**: It is to be noted that Ludium’s service must be readily available and guarantee the ease of use at the consumer level. For this, the current architecture uses zkTLS oracle to the minimal extent. Once we can be ensured that the system is stable, it is certainly possible to entertain more ideas including fiat off ramp (eg. Builder Payment in Fiat), integrations with diverse builder resume sources, and even automated work verification via zkML to minimize the validator’s activity
\*\* **Note 2**: We have not fully tested zkon to the fullest extent. From the experience with other zkTLS Oracle API such as Reclaim Protocol and zkPass, we assumed that it would be more readily available to utilize the existing API on Mina Protocol which was ZKON. However, if it comes down to unstable usage, we may need to develop the zkTLS framework on our own using Mina protocol as the zk Prover / Verifier network.

# Timeline / Budget

## Timeline

|  | Description | Estimated Time |
| --- | ----------- | -------------- |
| zkTLS Oracle Testing | Develop the zkTLS Oracle backend so that it can be tested to see if the data can be integrated and looped into the system | 2 Months |
| Portal Integration | zkTLS Oracle is fully integrated with the portal. It should trigger EVM smart contract based on the validator’s approval | 1 Month |
| Go to Market | Use the Escrow Payment service at work for Ludium’s event. For instance, Ludium is planning on participating in [Blockchain World Expo](https://x.com/web25_world/status/1884151580754391219) in Japan during June as a demoday partner. We are planning on opening up a IRL Launchpad where projects can crowd fund using fiat during the IRL event. | 1 Month |

## Budget

| <br> | **Description** | **Work Hours** | **Budget**<br>**(in $MINA)** |
| --- | ----------- | ---------- | ---------------- |
| **zkTLS Oracle Testing** | Fullstack - Technical lead who can oversight and manage the entire project | 150 | 18,000 |
| <br> | Designer - Design the page that integrates zkTLS page aligned with the existing portal branding | 50 | 6,000 |
| <br> | Backend - Develop a system that utilizes zkTLS pulling PG Service API and Binance API | 100 | 12,000 |
| <br> | Frontend - Develop the frontend page for testing later to be integrated with the portal | 50 | 6,000 |
| **Portal Integration** | Backend - Integrate escrow contract and the portal functions with the zkTLS Oracle | 50 | 6,000 |
| **Go To Market** | Project Lead - Recruit projects, onboard sponsor, mange projects, make connections | 150 | 18,000 |
| <br> | Designer - Design event details pages, announcement posters, slides, and others | 50 | 6,000 |
| <br> | Marketing - Social channel (ex. twitter, youtube) management and content distribution | 50 | 6,000 |
| <br> | Operation - Demoday preparation and execution in Japan / financial management | 100 | 12000 |
| **Total** | <br> | <br> | **90,000 $MINA** |

# Team

* **Ludium:** Web3 builder community that provides opportunities to the builders through education, incubation, investment and recruitment.

    | **[Website](https://ludium.world/)** | **[Twitter](https://twitter.com/ludium_official)** | **[Youtube](https://www.youtube.com/@Ludium)** | **[LinkedIn](https://www.linkedin.com/in/ludium-%EB%A3%A8%EB%94%94%EC%9B%80-3613aa292/)** |
    | ------- | ------- | ------- | -------- |
    | **[Discord](https://discord.com/invite/c8Snswayuw)** | **[Github](https://github.com/Ludium-Official)** | **[Deck](https://drive.google.com/file/d/1vtromU8KIKzvxaM0udoMO8QZ7ma3SYrb/view)** |  |
* **Habsida**: Habsida is a global developer bootcamp / agency that provides reliable IT solutions. The company will be responsible for developing the consumer ready product through planning / frontend / backend integrations. (**[See the Website](https://habsida.com/forcompanies)**)
* **Robert Seo**: Robert is a smart contract / blockchain backend developer. He will be mainly responsible for the Escrow contract development and leadnig the zkTLS integration (**[See Github](https://github.com/hex-aragon)**)
* **Ye Yoon Moon**: Ye Yoon is a member of Blockchain at Yonsei. She took Mina developer courses through Mina Korea team. She will be helping zkTLS integreation and backend data scheme for the payment integration (**[See CV](https://warp-acai-697.notion.site/)**)
* **POC:** Agwn, CEO of Ludium

    | **[Twitter](https://twitter.com/Ludium_Agwn)** | **[LinkedIn](https://www.linkedin.com/in/agwn/)** | **[Github](https://github.com/LudiumAgwn)** |
    | ------- | -------- | ------ |
    | **[Telegram](https://t.me/ludium_agwn)** | **[Email](mailto:agwn@ludium.community)** | **[Calendly](https://calendly.com/agwn/60-minute-meeting)** |

# Risk / Mitigations

* **Legal Issues:** Private payment and fiat on-off ramp is legally in the grey area. However, there are other services in Korea, such as [Overflex](https://over.network/overflex), already integrated fiat on-ramp via wechat, Alipay and Paypal. Although that cannot be a full endorsement, we see it as an enough assurance for execution. Meanwhile, we are undergoing legal consultation to make the zkTLS Escrow to be a legitimate business
* **Reliance on API:** The data needs to be provided by PG and Binance APIs which are outside of the Ludium’s control. However, considering the ease of use \*\*\*\*
* **zkTLS verification time:** Since our zkTLS system heavily relies on ZKON API, stability of the oracle network is critical for the development. With the 3 minute Mina Blocktime, it is to be tested whether the information feedback works smoothly to the extent that it can be used at the consumer level. If it comes downs to the conclusion that it is not reliable, it is possible that Ludium may have to develop API using Mina curcuit on our own.
* **Reliance on Ludium Backend:** As it can be noted, most of the system relies on Ludium’s backend, some are automated while others required human intervention. We believe it will take some time to ensure systematic integrity before we take bolder steps into the [Autonomous Escrow System](https://www.notion.so/241223-Autonomous-Grant-Agent-Roadmap-16539efa131f80e5887bc4d37943c61f?pvs=21) that is both automated and decentralized
