# infra-role-web3signer

This role configures [web3signer](https://docs.web3signer.consensys.net/) using docker

## Prerequisite

- docker
- check <https://github.com/status-im/infra-role-bootstrap-linux/>

### Dependency

- Postgresql database if `--slashing-protection-enabled` is enable
  - Ref: [slashing-protection](https://docs.web3signer.consensys.net/concepts/slashing-protection)

### Configuration

- Enable slashing protection: `web3signer_slashing_protection_enabled: true`
- Add keys to files (`files/keys/keys-1.yaml`), keys file extension should be `.yaml`. web3signer can't load `.yml` extension
- or Provide keys as variable
  - Ref: [web3signer keyfile](https://docs.web3signer.consensys.net/reference/key-config-file-params)

  - Example of key file content

  ```yml
  web3signer_keys:
    key-1:
      type: 'file-raw'
      keyType: 'BLS'
      privateKey: '0x25b1166a43c109cb330af8945d364722757c65ed2bfed5444b5a2f057f82d391'
  ```

- Check web3signer is up and running via API
  - [REST API](https://docs.web3signer.consensys.net/reference/api/rest)
  - Health Check - `curl -X GET http://127.0.0.1:9000/healthcheck`
  - List of public keys - `curl -X GET http://127.0.0.1:9000/api/v1/eth2/publicKeys`

### Playbook example

```yml
---
- name: Install web3signer
  hosts: 'sandbox'
  become: true
  roles:
    - {role: infra-role-web3signer}
  vars:
    web3signer_keys:
      key-1:
        type: 'file-raw'
        keyType: 'BLS'
        privateKey: '0x25b1166a43c109cb330af8945d364722757c65ed2bfed5444b5a2f057f82d391'

```

---

### Ref

- [consensy ansible web3signer](https://github.com/Consensys/ansible-role-web3signer)
- [signers_docker_compose](https://github.com/usmansaleem/signers_docker_compose)
