---
title: "Chain"
slug: "chain"
excerpt: "Executing an organized attack"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 15:17:54 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jul 05 2022 13:46:08 GMT+0000 (Coordinated Universal Time)"
---
A chain is an unordered collection of procedures files. Think of a chain in video game terms; it is  
an empty profile or shell, and it gets more powerful as you add specific abilities to it.

### Content

#### id

A unique identifier for that chain

#### metadata

This field contains information about the chain such as who created it, when it was released, etc.

##### variables

They are a list of parameters that are needed for the chain to run correctly. It could be a path to a file, an api key to authorize to a certain service, etc.

#### name

The display name of the chain.

#### description

A description of what that chain does and how it does it

#### ttps

A list of TTP used by the chain to accomplish its goal.

#### ordered

A boolean that indicates if the list of TTPS needs to be executed in order or not.

#### platforms

A list of platform on which the chain can be executed.

#### executors

A list of executor that can run that chain.

### TTP Tuesday

***

Every Tuesday, Prelude security engineers release a new chain in an event called TTP Tuesday. These chains  
typically align to threat intelligence and are loaded into Operator automatically for Professional license holders. You can view past chains on our [chains website](https://chains.prelude.org).

### Build your own chain

***

You can build your own chains through the Launch Chain sidebar inside Operator. Design your chains on real-world threat actors (APT group) or detection rules you want to test. Alternatively, you can build chains manually by applying a chain property to any TTP YML file manually. Example below.

```yml
id: 4e707752-4abc-4799-9ff3-0caddc032bc2
metadata:
  license: community
  authors:
  - khyberspache
  tags: []
  chains:
  - My Custom Chain

...
```
