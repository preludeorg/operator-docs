---
title: "TTP"
slug: "ttp"
excerpt: "ATT&CK-based tactics, techniques and procedures"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 15:18:11 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Thu Nov 24 2022 00:53:51 GMT+0000 (Coordinated Universal Time)"
---
A TTP (Tactics, Techniques, and Procedures) is a specific ATT&CK technique implementation. Each TTP defines an independent ability a chain could contain, along with classification details describing what operating systems it will work on. Prelude natively supports Windows, Linux and MacOS (darwin) platforms and a series of shell and non-shell executors (i.e., the things that run the commands).

### How it works

***

When you deploy a chain against a range of agents, Operator will look at each TTP inside the chain and match up the platforms and executors to the agent. It first checks for an exact match of platform and executor. If none are found, it checks the global platform for a matching executor. Only if a match is found will the TTP be sent to the agent.

### Supported platforms & executors

***

There are three supported platforms: Windows, Linux and Darwin (another word for MacOS). For each platform, there are a number of available executors. Not every executor will work on every platform, just as a Linux shell script won't work on Windows. When you build a custom TTP, you can assign it an existing executor or you can create a new one - your agent just needs to understand how to work with it (as the executor is sent alongside the command).

Below are some common executors you'll see in Operator:

- sh: shell command
- bash: Bash shell command
- psh: Powershell
- pwsh: PowerShell core
- python: Python script
- node: Node script
- keyword: user-defined ([read our blog post](https://feed.prelude.org/p/keywords-to-the-kingdom-simple-modular))

### Community license

***

Prelude ships with an open-source collection of TTP files with the Community license. Your application will check at start up for any new TTPs merged into Community and load them automatically. If you want to add your own procedure files, you can either submit pull requests to Community or create similar YML files locally.

### Professional license

***

There is a closed-source Professional license which is available under our licensing options in the Settings section. This repository contains additional TTPs. The TTPs also contain additional non-shell executors not available in Community.
