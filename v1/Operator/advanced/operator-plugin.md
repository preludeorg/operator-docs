---
title: "Plugin"
slug: "operator-plugin"
excerpt: "Extend the framework in any direction"
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 14:41:50 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Tue Jul 05 2022 13:38:39 GMT+0000 (Coordinated Universal Time)"
---
A plugin is a separate module of code that can literally plug into the framework to extend the core functionality. Popular examples of plugins are new UI components, dashboards, and new ways of reporting information or displaying data.

### Beware of untrusted plugins

***

Because plugins are arbitrary javascript files, you should never upload a plugin from someone you do not trust, unless you have personally read and understood the code.

### Create your own plugin

***

You can write your own custom plugin easily. Plugins must be javascript files, which can contain JavaScript (jQuery and NodeJS supported). You can view open-source plugins in the [Community](https://github.com/preludeorg/community) repository. Plugins can interact with the core system through the internal REST API or the Basic interface. Basic interface methods are shown below.

#### Available internal functions

***

- Basic.exists(file)
- Basic.createStorage([directories])
- Basic.normalizePath(file)
- Basic.storeData(contents, path)
- Basic.loadData(path)
- Basic.loadYaml(path)
- Basic.deleteData(path)
- Basic.deleteDir(directory)
- Basic.recursiveFiles(directory)
- Basic.uuidv4()
- Basic.isUUID(string)
- Basic.bin2string([bytes])
- Basic.deepCopy(object)
- Basic.constructEndpoint(endpoint, parameters)
- Basic.nullValues(array)
- Requests.fetchOperator(endpoint, parameters)
- Requests.fetchGatekeeper(endpoint, parameters)

### Hello world plugin

***

You can create your own plugins quickly by writing javascript files, which Operator loads when booting up. Plugins are stored in your workspace. 

#### Example: Save this plugin as hello.js and add it to your workspace

A plugin javascript file.

```javascript
alert('Hello world!');
```

A corresponding configuration file for this plugin.

```yml
name: Hello
description: Say hello when you start Operator
```
