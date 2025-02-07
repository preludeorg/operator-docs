---
title: "Vectr"
slug: "vectr"
excerpt: ""
hidden: false
metadata: 
  image: []
  robots: "index"
createdAt: "Wed Jun 29 2022 17:00:31 GMT+0000 (Coordinated Universal Time)"
updatedAt: "Wed Jun 29 2022 17:00:31 GMT+0000 (Coordinated Universal Time)"
---
### What is Vectr?

***

Vectr ([Github](https://github.com/SecurityRiskAdvisors/VECTR)) is a tool that facilitates tracking of your red and blue team testing activities to measure detection and prevention capabilities across different attack scenarios.

### What does the Vectr plugin do?

***

The Vectr plugin will automatically send your executed TTP data to Vectr in real-time. A top-level Prelude assessment is created in Vectr, then campaigns are configured in one of 2 ways depending upon how you configure the campaign value. If the campaign field is left blank or set to the default "automatic" value, every click of the `Deploy` button in Operator will create a new timestamped campaign in Vectr. If the campaign value is manually specified, then TTP data will append to that specific campaign.

### Configuring the plugin

***

First, go the setting and click on Vectr plugin to install it. Next, you must configure your settings:

- **macOS:** ~/Library/Application\\ Support/Operator/portal.prelude.org/plugins/Vectr/config.yml
- **linux:** ~/.config/Operator/portal.prelude.org/plugins/Vectr/config.yml
- **Windows:** %APPDATA%\\Operator\\portal.prelude.org\\plugins\\Vectr\\config.yml

Update your `config.yml` file to have your correct settings under the `config` object:

```yaml
config:
  url: https://sravectr.internal:8081
  database: PURPLE_DEMO_CE
  org_name: MITRE
  key_id: OSDZXU77OZSB8DXEAQK4VG
  secret_key: Rl5i3b0gdhPgu/4+Ooa+MofmvWwFRyOfAGwrqEayWk8=
  campaign: automatic
```

Configure the optional campaign field. If the campaign value is manually specified, then TTP data will append to that specific campaign. Otherwise, Operator will generate a new campaign automatically for each `Deploy`:

- campaign: automatic
