# infra-role-web3signer

This role configurs[web3signer](https://docs.web3signer.consensys.net/) using docker

## Prerequisite

- docker
- check <https://github.com/status-im/infra-role-bootstrap-linux/>

## Dependency

- Postgresql if g --slashing-protection-enabled is enable
- <https://docs.web3signer.consensys.net/concepts/slashing-protection>

### Configuration

- Enable slashing protection: `w33signer_slashing_protection_enabled: true`
- Add keys to files or provide keys as variable

```yml
key-1:
  type: 'file-raw'
  keyType: 'BLS'
  privateKey: '0x25b1166a43c109cb330af8945d364722757c65ed2bfed5444b5a2f057f82d391'
```

## Playbook example

```yml
---
- name: Install web3signer
  hosts: 'sandbox'
  become: true
  roles:
    - {role: infra-role-web3signer}
```
