---
sip: <to be assigned>
title: Terminal SNX Inflation
status: WIP
author: Vance Spencer (@FrameworkVance), Deltatiger (@deltatigernz), Michael Anderson (@meanderson)
discussions-to: governance

created: 2019-10-25
requires: Inflation Smoothing (SIP# TBD)

---

<!--You can leave these HTML comments in your merged SIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new SIPs. Note that an SIP number will be assigned by an editor. When opening a pull request to submit your SIP, please use an abbreviated title in the filename, `sip-draft_title_abbrev.md`. The title should be 44 characters or less.-->


## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the SIP.-->
This proposal will add a perpetual weekly reward of 100,000 SNX starting on June 21, 2023, the 222nd week on the SNX inflation schedule. 

This SIP is the formal spec successor of deltatiger's [Draft SIP Proposal #36](https://github.com/Synthetixio/SIPs/issues/36), specifically pertaining to terminal inflation. 


## Abstract
<!--A short (~200 word) description of the technical issue being addressed.-->
- Terminal inflation is an important mechanism to keep the SNX protocol stable in perpetuity
- With the original inflation schedule, weekly inflation drops from 90.1K to 0 on March 13, 2024
- With inflation smoothing as described in SIP # TBD, weekly inflation drops below 100K on June 21, 2023 

## Motivation
<!--The motivation is critical for SIPs that want to change Synthetix. It should clearly explain why the existing protocol specification is inadequate to address the problem that the SIP solves. SIP submissions without sufficient motivation may be rejected outright.-->
Perpetual weekly inflation serves as a mechanism to keep the protocol stable for the long term


## Specification
<!--The technical specification should describe the syntax and semantics of any new feature.-->
Adjust [SupplySchedule.sol](https://github.com/Synthetixio/synthetix/blob/master/contracts/SupplySchedule.sol) to account for the following changes:
- Starting on June 21, 2023, the weekly issuance of SNX tokens will adjust to 100,000.
- This model will stay in place until it is stopped or adjusted.

With Inflation Smoothing and 100K Terminal Inflation:
![image](https://media.discordapp.net/attachments/637348888713625626/637736129013088295/Screen_Shot_2019-10-26_at_12.20.50_PM.png)

With Original Schedule and 100K Terminal Inflation
![image](https://media.discordapp.net/attachments/637348888713625626/637735914516512788/Screen_Shot_2019-10-26_at_12.24.34_PM.png)

[Model](https://docs.google.com/spreadsheets/d/1rVXFnZSMvHEv5XpA5Q23x-cXEo7w-2T80wlAfT-YbuI/edit#gid=1640166717)


## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->
Perpetual weekly inflation serves as a mechanism to avoid scenarios that would adversely impact the protocol like:

- Minters packing up at the same time due to a lack of rewards
- Synth supply shrinking
- SNX unlocking to be sold down
- SNX price dropping
- sETH LPs getting their income halved and also now dropping in value
- sETH LPs exiting by withdrawing and converting sETH to ETH
- sETH getting smashed out of peg
- Arb pool being unattractive as SNX drops relative to ETH

## Test Cases
<!--Test cases for an implementation are mandatory for SIPs but can be included with the implementation..-->
Standard test cases for Solidity contract compling and deploying onto Ethereum testnets before updating the contract on mainnet. 

## Implementation
<!--The implementations must be completed before any SIP is given status "Implemented", but it need not be completed before the SIP is "Approved". While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.-->
- Update and deploy [SupplySchedule.sol](https://github.com/Synthetixio/synthetix/blob/master/contracts/SupplySchedule.sol) to Ropsten, Rinkby, and Kovan
- Update and deploy changes to proxy contracts that reference SupplySchedule.sol on Ethereum testnets
- Update and deploy [SupplySchedule.sol](https://github.com/Synthetixio/synthetix/blob/master/contracts/SupplySchedule.sol) to Ethereum mainnet
- Update and deploy changes to Ethereum mainnet proxy contracts that reference SupplySchedule.sol

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
