---
title: "Outpost"
slug: "outpost"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Mon Aug 08 2022 04:26:36 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Fri Feb 24 2023 23:13:23 GMT+0000 (Coordinated Universal Time)"
---
Outpost serves a file system (bucket) of resources - TTPs, payloads, plugins, docs and training modules - which  
are synced with all Operator instances which have access. Prelude serves two Outpost servers to the public,  
each supplying a bucket of content for their respective license. As a user, when you start Operator you immediately sync with the Outpost server your license allows.

Enterprise organizations have the option of serving their own Outpost, allowing them to share private content across any seat in their account. To do this:

1. Update the conf/.yml file for your chosen environment. 
2. Start Outpost and verify through the unauthenticated :9752/ping endpoint that the content is being served.
3. Inside Operator's Connect section, plug in your host + token in the Outpost configuration panel.
4. Verify each seat in the organization can see the content in the Outpost.

> Once you connect Operator to your Outpost, every member of your org will automatically start publishing  
> their results to the SIEM you configured in the environment file. Splunk, Elastic, and Vectr are the  
> built-in options, and users are able to add additional/different SIEMs beyond these.

### Download

At this time, Outpost's source code is only provided to Enterprise customers. Please reach out to your support contact or [support@preludesecurity.com](mailto:support@preludesecurity.com) for access. 

### Installation

Outpost requires Python 3.8+. 

```
pip install -r requirements.txt
python server.py
```

> Note the workspace location that will store all your Operator resources

### Publishers (optional)

Outpost can be backed by a data store which will persist your Operator results (links). 

Data storage is optional when running your own Outpost but recommended if you want to aggregate the data from  
all Operator seats in your organization. To set up a publisher, start by examining those available in the conf/\*  
environment files. Add configuration details then start Outpost with the publisher:

```
python server.py -D /tmp/community -P elastic
```
