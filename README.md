# Founder’s Table - IRL Builder Launchpad

## Overview

![Founder's Table Poster](./images/1_1%20poster.png)

Founder’s table is a series of global Demoday event for Web3 project at various stages. Seven prominent projects are selected across all chains and domains to pitch their project to raise their value to the next stage. The following repo describes the system design and codes required to set up a Founder’s Table on [Ludium Portal](https://www.ludium.world/)

# System Architecture

![Founder's Table System Architecture](./images/Founder's%20Table.png)

Founder’s table page includes four features

- **Admin Initiate the Program:** Approved accounts, initially Admin account, are able to initiate the Founder’s Program. Theoretically, it is possible to allow any account to launch the program but for the current version, we are limiting the ability to specific accounts for the purpose of the quality assurance. Admin can set the conditions for the program including the limit of total amount, number of shares allowed to purchase per account, total duration, and other requirement for the program.
- **Projects Submit Application:** Once the program is set up, projects can submit applications that include name, description, links, total amount asked, price of each share,  milestones and terms, Due Dates, and other important information necessary for the supporters to know
- **Validators Select Projects:** Validators review the submitted application and conduct due diligence process. Validators are most likely to be incubators and/or other organizations who recommended the projects to the program
- **Supporters Buy Shares:** Supporters can participate in the offline event, view the page, and support the project they like by buying shares. Shares include executable rights such as Equity, Bond, Token(s), Revenue Shares, Claimable Services and/or other financial/non-financial incentives. The amount that each supporter can spend to buy shares depends on the conditions set by the Admin during the program initiation
- **Projects Deliver Milestones:** Projects are required to deliver milestones in order to receive the amount locked in through buying shares. Projects submit milestones as they set out in the terms which are reviewed by the validators to ensure that the delivery is completed. Once the delivery is confirmed, escrow contract unlocks the amount proportional to the milestone
- **Terms Are Settled:** After all milestones are delivered, settlement is completed and the program is finished

# ZKP2P Fiat On Ramp

![ZKP2P Fiat On Ramp](./images/zkp2p.png)

(Reference from [ZKP2P V2 Protocol Diagram](https://docs.zkp2p.xyz/developer/the-zkp2p-v2-protocol))

Unlike the other launchpad, the experience of IRL event can be more experiential, trust-generating, and sporadic at the same time. Ludium intend the experience of attending the demoday to be like going to an amusement park or a concert where audiences are given easy access to get to know a new project and support them on the spot. For this reason, we believe ease of payment via fiat on ramp is crucial to increase the adoption.

In order to activate the fiat on ramp experience, we are integrating zkp2p escrow payment which support 25 different FIAT currency payment via Venmo, Wise and other payment options. The integration is basically the same as integrating any 3rd party escrow payment service on top of the Ludium’s direct crypto payment. All fund paid in Fiat are stored as $USDT/USDC on the program treasury later to be unlocked in accordance with the system architecture