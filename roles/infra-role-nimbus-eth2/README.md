# infra-role-nimbus

This role configurs beacon node using [Nimbus Eth2](https://nimbus.guide/) using docker
Ethereum Consensus Layer node

## Prerequisite

- docker

### Configuration  (To be updated)

- Provide path of the eth1 JWT secret if eth1 client is running on same machine

```yml
nimbus_eth2_eth1_jwt_secret_enabled: true
eth1_jwt_secret_path: '/docker/nethermind/node/keys/jwtsecret'
```

- Or Manually copy jwtsecret here
  - Check Nethermind <https://docs.nethermind.io/get-started/consensus-clients/#configuring-json-rpc-interface/>

```yml
nimbus_eth2_eth1_jwt_secret_copied: true
eth1_jwt_secret: '15547afb5e5cc621ade54c6b00c157d5b39a213fedd87bc80b2ead7baaa530d7'
```

## Playbook example

```yml
---
- name: Install Nimbus
  hosts: 'sandbox'
  become: true
  roles:
    - {role: infra-role-nimbus-eth2}
```
