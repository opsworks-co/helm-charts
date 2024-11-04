# vault-backup
## Pre-requirements
### Prepare Vault user
Create policy:
```
vault login
cat <<EOF | vault policy write vault-backup -
path "sys/storage/raft/snapshot" {
  capabilities = ["read"]
}
EOF
```
Create token:
```
vault token create -period=24h -policy=vault-backup
```

## Installing chart
```sh
helm upgrade --install vault-backup opsworks/vault-backup --set vault.token=mytoken
```

## Decrypt the snapshot
```sh
gpg --batch --yes --passphrase ${ENCRYPTION_PASSWORD} -d --output decrypted.txt  encrypted.txt
```