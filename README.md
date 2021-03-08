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
```

Copy vagrant file from `vagrant/examples/` and then create the vagrant box (you can change to `--provider=libvirt` if you want to use Libvirt provider):
```
$ cp -v vagrant/examples/Vagrantfile.zabbix-box.fedora-33.x86_64.example vagrant/Vagrantfile.zabbix-box
$ vagrant up --provider=virtualbox
```

Provision the vagrant box:
```
$ vagrant ssh zabbix-box -- sudo salt-call state.highstate
```

Deploy Zabbix Server, Web, Agent, and Postgres containers:
```
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.config
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.config.nginx
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.service.postgres
$ vagrant ssh zabbix-box -- sudo salt-call state.sls zabbix.service.server
```

To access Zabbix web, go to https://zabbix-box. Use the following default username and password:
* Username: `Admin`
* Password: `zabbix`

Go to [Configuration > Hosts](https://zabbix-box/hosts.php) and rename host from `Zabbix server` to `zabbix-server-pod`.


## Slack Notifications

Visit https://api.slack.com and then create an app with the following `Bot Token Scopes`:
* `incoming-webhook`
* `chat:write.public`
* `chat:write.customize`
* `chat:write`

On your `zabbix-box` web-page, go to `Administration` > `Media types` > `Slack` and set `bot_token` value using your apps `OAuth Access Token` ("`xoxp-...`").


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


## Allow Guests to view graphs and screens

1. Go to `Administration` > `User groups` and select `Guests`.
1. Go to `Permissions` tab and add a `Host Group` for example `Linux servers` with permission `Read`.
1. Click `Add` and then click `Update`.
