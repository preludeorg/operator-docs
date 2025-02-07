---
title: "Brain"
slug: "brain"
excerpt: "Intelligent Decision-Making At Scale"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 14:20:51 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Feb 17 2023 17:21:06 GMT+0000 (Coordinated Universal Time)"
---
The planner is a multi-level finite state machine which determines the TTP order when a chain is deployed. The  
procedures inside a chain are naturally unordered. Once deployed, it looks at the planner for a decision every time a decision is needed. The finite state algorithm organizes all TTPs into a _kill-chain_ based by ATT&CK tactic and then again by technique. Then, it executes one tactic at a time until it exhausts all TTP files in a given chain.

### Always learning

***

When a chain executes, it collects information which Operator can learn from. As this info is processed, it is fed back into the planner, often opening up a previously closed state. For example, say the planner is currently busy executing decisions for a chain, which has completed the first two tactical states above, and it is executing procedures under Discovery. If the planner learns something which can unlock a "defense evasion" procedure, it will instruct the chain to drop out of the discovery state and into the defense evasion one in order to do the newly discovered action.
