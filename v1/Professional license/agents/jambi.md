---
title: "Jambi"
slug: "jambi"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Sun Aug 07 2022 07:01:48 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Sun Aug 07 2022 07:03:21 GMT+0000 (Coordinated Universal Time)"
---
Jambi is a fully modular Powershell agent which enables in-memory operations on Windows.

### Supported Protocols

Jambi supports HTTP and HTTPS. 

### Starting Jambi

`powershell .\jambi.ps1 -Address http://192.168.1.1:3391 -Contact http -Name "Demo" -Debug`  
This will launch an agent that will connect to the server at 192.168.1.1 on port 3391 with the given arguments.

### Parameters

- Address: The remote server (Operator) IP Address. Defaults to http\://localhost:3391.
- Contact: The protocol used to the connect to the remote server. Defaults to HTTP.
- Name: The name of the agent. Defaults to a random UUID.
- Sleep: The sleep interval for the agent. Defaults to 30.
- ModuleURI: The path to look for modules to resolve. Defaults to "/payloads/jambi/v1.7/modules/".
- Debug: Enables additional debug logging. Defaults to false. 

### Included Modules

- Jambi-HostRecon: Performs local host and network enumeration. 
- Jambi-LoadPatchType: Creates a "JambiPatcher" [.NET type](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/add-type). 
- Jambi-PatchAMSI: Patches AMSI in the current thread, enabling other Powershell commands to be  
  launched without having those scripts scanned.
- Jambi-PatchETW: Patches ETW in the current thread, enabling other Powershell commands to be launched without emitting events.
- Jambi-RunPsh: Run Powershell commands in the current Powershell process. 

### Invoking modules in a TTP

Format your TTP to invoke the modules by including the module name as the first parameter of the command. For example, to perform host enumeration, structure your TTP like this example: 

```yaml
platforms:
    windows:
        psh:
            command: Jambi-HostRecon -DisableDomainChecks
```

For more examples, see the chain [Jambi Modules](https://chains.prelude.org/chains/510bcbab-b7c9-4edd-bab9-3fe4f9ae2f66/jambi-modules) and the associated TTPs.
