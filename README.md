# Project Oni 👹

Our mandate is:

> To verify the successful end-to-end outcome of the filecoin protocol and filecoin implementations, under a variety of real-world and simulated scenarios. 

➡️  Find out more about our goals, requirements, execution plan, and team culture, in our [Project Description](https://docs.google.com/document/d/16jYL--EWYpJhxT9bakYq7ZBGLQ9SB940Wd1lTDOAbNE).

## Testing topics

These are the topics we are currently centering our testing efforts on. Our testing efforts include fault induction, stress tests, and end-to-end testing.

* **slashing:**
    * We are recreating the scenarios that lead to slashing, as they are not readily seen in mono-client testnets.
    * Context: slashing is the negative economic consequence of penalising a miner that has breached protocol by deducing FIL and/or removing their power from the network.
* **windowed PoSt/sector proving faults:**
    * We are recreating the proving fault scenarios and triggering them in an accelerated fasion (by modifying the system configuration), so that we're able to verify that the sector state transitions properly through the different milestones (temporary faults, termination, etc.), and under chain fork conditions.
    * Context: every 24 hours there are 36 windows where miners need to submit their proofs of sector liveness, correctness, and validity. Failure to do so will mark a sector as faulted, and will eventually terminate the sector, triggering slashing consequences for the miner.
* **syncing/fork selection:**
    * Newly bootstrapped clients, and paused-then-resumed clients, are able to latch on to the correct chain even in the presence of a large number of forks in the network, either in the present, or throughout history.
* **present-time mining/tipset assembly:**
    * Induce forks in the network, create network partitions, simulate chain halts, long-range forks, etc. Stage many kinds of convoluted chain shapes, and network partitions, and ensure that miners are always able to arrive to consensus when disruptions subside.
* **catch-up/rush mining:** 
    * Induce network-wide, or partition-wide arrests, and investigate what the resulting chain is after the system is allowed to recover.
    * Context: catch-up/rush mining is a dedicated pathway in the mining logic that brings the chain up to speed with present time, in order to recover from network halts. Basically it entails producing backdated blocks in a hot loop. Imagine all miners recover in unison from a network-wide disruption; miners will produce blocks for their winning rounds, and will label losing rounds as _null rounds_. In the current implementation, there is no time for block propagation, so miners will produce solo-chains, and the assumption is that when all these chains hit the network, the _fork choice rule_ will pick the heaviest one. Unfortunately this process is brittle and unbalanced, as it favours the miner that held the highest power before the disruption commenced.
* **storage and retrieval deals:**
    * end-to-end flows where clients store and retrieve pieces from miners, including stress testing the system.
* **payment channels:**
    * stress testing payment channels via excessive lane creation, excessive payment voucher atomisation, and redemption.
* **drand incidents and impact on the filecoin network/protocol/chain:** 
    * drand total unavailabilities, drand catch-ups, drand slowness, etc.
* **mempool message selection:** 
    * soundness of message selection logic; potentially targeted attacks against miners by flooding their message pools with different kinds of messages.
* **presealing:** 
    * TBD, anything related to this worth testing?

## Team composition

* [@raulk](https://github.com/raulk) (Captain + TL)
* [@nonsense](https://github.com/nonsense) (Testground TG + engineer)
* [@yusefnapora](https://github.com/yusefnapora) (engineer and technical writer)
* [@vyzo](https://github.com/vyzo) (engineer)
* [@schomatis](https://github.com/schomatis) (advisor)
