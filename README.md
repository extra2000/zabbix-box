# zabbix-box

| License | Versioning | Build |
| ------- | ---------- | ----- |
| [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) | [![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release) | [![Build status](https://ci.appveyor.com/api/projects/status/fsr74lorx5h1ht58/branch/master?svg=true)](https://ci.appveyor.com/project/nikAizuddin/zabbix-box/branch/master) |

Developer box for [Zabbix](https://github.com/zabbix/zabbix).


## Getting Started

Clone this repository and `cd`:
```
$ git clone --recursive https://github.com/extra2000/zabbix-box.git
$ cd zabbix-box
```


## Creating Vagrant Box

Copy example pillar file for Zabbix and NGINX. Optionally you may want to edit the values in the pillar files:
```
$ cp -v salt/roots/pillar/zabbix.sls.example salt/roots/pillar/zabbix.sls
$ cp -v salt/roots/pillar/nginx.sls.example salt/roots/pillar/nginx.sls
$ cp -v salt/roots/pillar/zabbix-agent.sls.example salt/roots/pillar/zabbix-agent.sls
```

Copy vagrant file from `vagrant/examples/` and then create the vagrant box (you can change to `--provider=libvirt` if you want to use Libvirt provider):
```
$ cp -v vagrant/examples/Vagrantfile.zabbix-box.fedora-33.x86_64.example vagrant/Vagrantfile.zabbix-box
$ vagrant up --provider=virtualbox
```

Set vagrant box timezone (use `$ vagrant ssh zabbix-box -- timedatectl list-timezones` to get a list of available continents and regions):
```
$ vagrant ssh zabbix-box -- sudo timedatectl set-timezone [CONTINENT/REGION]
```

Provision the vagrant box:
```
$ vagrant ssh zabbix-box -- sudo salt-call state.highstate
```

Deploy Zabbix Server, Web, Agent, and Postgres containers:
```
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.config
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.service.postgres
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.service.server
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix_agent
```

Configure and deploy NGINX for HTTPS:
```
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.config.nginx,nginx.service
```

To access Zabbix web, go to https://zabbix-box. Use the following default username and password:
* Username: `Admin`
* Password: `zabbix`


## Configure Global Macros

Go to `Administration` > `General` > `Macros`, add the following macros:
| Macro | Value |
| --- | --- |
| `{$ZABBIX.URL}` | https://zabbix-box |


## Slack Notifications

Visit https://api.slack.com and then create an app, for example named `myzabbix-bot`, with the following `Bot Token Scopes`:
* `chat:write`

On your Slack workspace, create a Slack channel for the Zabbix notification, for example `#zabbix`. Then, on your channel's `More options` select `Add apps` and add your bot `myzabbix-bot` into your channel.

On your `zabbix-box` web-page, go to `Administration` > `Media types` > `Slack` and do the followings:
1. Set `bot_token` value using your apps `OAuth Access Token` ("`xoxb-...`").
1. Set `slack_mode` value to `event` because Zabbix seems unable to reply to a message.
1. To fix duplicated notifications due to `Slack notification failed : invalid_auth`, go to `Options` and set `Attempts` to `1`.

To `test` Slack Notification, use the following values (replace `#zabbix` with your Slack channel):
* channel: `#zabbix`
* event_id: 1
* event_nseverity: 1
* event_source: 0
* event_update_status: 0
* event_value: 1
* trigger_id: 1
* zabbix_url: https://zabbix-box

You may want to read the Zabbix Slack integration official documentations at https://git.zabbix.com/projects/ZBX/repos/zabbix/browse/templates/media/slack/README.md


## Enabling Notications

Make sure disable all unused `Media types` except `Slack` if you use Slack for notifications.

Enable `Media` for Admin user. Go to `Administration` > `Users` > `Admin` choose `Media` and add the following media (replace `#zabbix` with your Slack channel):
* Type: `Slack`
* Send to: `#zabbix`
* When active: `1-7,00:00-24:00`
* Use if severity:
    * [x] Not classified
    * [x] Information
    * [x] Warning
    * [x] Average
    * [x] High
    * [x] Disaster
* Enabled: `True`

Enable `Actions`. Go to `Configuration` > `Actions` > `Trigger actions`, enable `Report problems to Zabbix administrators`.


## Creating Vagrant box for Agent, for testing purpose

Deploy `zabbix-agent-box` from [extra2000/zabbix-agent-box](https://github.com/extra2000/zabbix-agent-box).

Go to https://zabbix-box/hosts.php?form=create:

* Under tab `Host`:
    * Host name: `zabbix-agent-box`
    * Groups: `Linux servers`
    * Interfaces:
        * Type: `Agent`
        * DNS Name: `zabbix-agent-box`
        * Connect to: `DNS`
        * Port: `10050`
* Under tab `Templates`:
    * Add `Template OS Linux by Zabbix agent active`, can be found in host group `Templates/Operating systems`.

Note that when using `agent active`, Zabbix server will query metrics from agent's port `10050`. If the agent is behind firewall or NAT, use passive agent template `Template OS Linux by Zabbix agent`.

## Allow Guests to view graphs and screens

1. Go to `Administration` > `User groups` and select `Guests`.
1. Go to `Permissions` tab and add a `Host Group` for example `Linux servers` with permission `Read`.
1. Click `Add` and then click `Update`.
