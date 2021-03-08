# Changelog

### [1.2.2](https://github.com/extra2000/zabbix-box/compare/v1.2.1...v1.2.2) (2021-03-08)


### Documentations

* **README:** Change agent instructions to add active check template instead of passive check template ([1028f63](https://github.com/extra2000/zabbix-box/commit/1028f63ee83ee4669dac01a1f530f86c1ff9e7a1))

### [1.2.1](https://github.com/extra2000/zabbix-box/compare/v1.2.0...v1.2.1) (2021-03-07)


### Documentations

* **vagrant:** Add comments for port forwarding ([0bf62a5](https://github.com/extra2000/zabbix-box/commit/0bf62a50348fe3bde33377ab4f4366f792fbfc8a))

## [1.2.0](https://github.com/extra2000/zabbix-box/compare/v1.1.1...v1.2.0) (2021-03-05)


### Features

* **submodule:** Update `zabbix-formula` to [v1.2.0](https://github.com/extra2000/zabbix-formula/releases/tag/v1.2.0) ([06489f6](https://github.com/extra2000/zabbix-box/commit/06489f69abfbff35f31844fced7a487eb1011def))


### Performance Improvements

* **vagrant:** Increase RAM from 1GB to 1.5GB ([fe9463b](https://github.com/extra2000/zabbix-box/commit/fe9463b7a034d61c7a7109a8eee967c02f426a2d))


### Code Refactoring

* **vagrant:** Remove Vagrant files for Zabbix agent ([aa58c0b](https://github.com/extra2000/zabbix-box/commit/aa58c0bce0710fd32cd744088d848828127a0ace))
* **vagrant:** Rename `vagrant/examples/server/` to `vagrant/examples/` ([f653aea](https://github.com/extra2000/zabbix-box/commit/f653aeae9a4114538640cd0025c7944166d63ed6))


### Continuous Integrations

* **AppVeyor:** Update instruction for copying Vagrant file ([a19504d](https://github.com/extra2000/zabbix-box/commit/a19504df2f4acbaf439fd4510e14948b9b72608f))


### Documentations

* **pillar/zabbix.sls.example:** Optimize container resources ([ef3cfdc](https://github.com/extra2000/zabbix-box/commit/ef3cfdc7fa923110698e516e9127f0e1acec4a24))
* **README:** Add instructions for setting `guests` permissions ([3404de3](https://github.com/extra2000/zabbix-box/commit/3404de3eb46daffe139ce63b35cbf232ff19033e))
* **README:** Simplify instructions for Zabbix agent and update other instructions ([2b10394](https://github.com/extra2000/zabbix-box/commit/2b1039489505889075a745f85f3a5011ea1740c4))

### [1.1.1](https://github.com/extra2000/zabbix-box/compare/v1.1.0...v1.1.1) (2021-03-01)


### Documentations

* **README:** Improve instructions and add instruction to create templates for the created Agent ([ef0071d](https://github.com/extra2000/zabbix-box/commit/ef0071d5d8ca739fa0e59178d4f8986d5445795c))

## [1.1.0](https://github.com/extra2000/zabbix-box/compare/v1.0.0...v1.1.0) (2021-03-01)


### Features

* **submodule:** Add [nginx-formula v1.0.0](https://github.com/extra2000/nginx-formula/releases/tag/v1.0.0) ([3649935](https://github.com/extra2000/zabbix-box/commit/3649935f0f600be47f549f10a88f7365067088ea))
* **submodule:** Update `zabbix-formula` to [v1.1.0](https://github.com/extra2000/zabbix-formula/releases/tag/v1.1.0) ([00d5c25](https://github.com/extra2000/zabbix-box/commit/00d5c259380c20de1bd9f217f277e0bf62e315a2))
* **vagrant:** Add Vagrant files for Zabbix agent ([1829736](https://github.com/extra2000/zabbix-box/commit/182973632209e23d9d2d77cfc509a8a24cc1588d))


### Documentations

* **README:** Add instruction for creating Zabbix agent box ([158cfd7](https://github.com/extra2000/zabbix-box/commit/158cfd718634e816a1e1777a4d8a09ec4ea18b36))
* **README:** Add instruction to configure NGINX for HTTPS and changed HTTP to HTTPS ([3e23556](https://github.com/extra2000/zabbix-box/commit/3e235569ba717f22b8b7e0fc38112375e33b6e8b))
* **README:** Add instruction to configure Slack Notifications ([faa63a2](https://github.com/extra2000/zabbix-box/commit/faa63a29b74772b7bd8e85b85e11a9c0974ae9aa))
* **README:** Add instruction to create NGINX pillar file ([a188bde](https://github.com/extra2000/zabbix-box/commit/a188bdee849d0df26132449a0a7e6e325b109b20))


### Continuous Integrations

* **AppVeyor:** Add instruction to create NGINX pillar file ([abcab99](https://github.com/extra2000/zabbix-box/commit/abcab9961f99cb66570c56012b79265fe23ac25b))

## 1.0.0 (2021-02-18)


### Features

* **salt:** Add implementations for `salt/` ([b4cf2dd](https://github.com/extra2000/zabbix-box/commit/b4cf2ddae96c782c45a692d4933a4b7237241af7))
* **submodule:** Add [podman-formula v2.2.1](https://github.com/extra2000/podman-formula/releases/tag/v2.2.1) ([c9921db](https://github.com/extra2000/zabbix-box/commit/c9921db74f9a6532aaa0cfef94d0cfb4d9257add))
* **submodule:** Add [zabbix-formula v1.0.0](https://github.com/extra2000/zabbix-formula/releases/tag/v1.0.0) ([b026690](https://github.com/extra2000/zabbix-box/commit/b026690a1a45bd70aabf3ebd494748edd488eed0))
* **vagrant:** Import Vagrant files from [extra2000/generic-box v1.5.0](https://github.com/extra2000/generic-box/releases/tag/v1.5.0) ([d937f64](https://github.com/extra2000/zabbix-box/commit/d937f647d8dbf942981e5cfb6abb8aa2d89e828a))


### Continuous Integrations

* Add AppVeyor with `semantic-release` bot ([cb6bf08](https://github.com/extra2000/zabbix-box/commit/cb6bf0875d6bedabc6bcf463a51e5e66960f16a0))


### Documentations

* **README:** Update `README.md` ([92d4182](https://github.com/extra2000/zabbix-box/commit/92d4182e0e15dc9b0825b2a829b187983063e6a1))
