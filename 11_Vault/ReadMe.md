# Vault

## Encrypting a file using it in a playbook
`ansible-vault --help`  
`ansible-vault encrypt [file name]`  
`ansible-vault view [file name]`  
`ansible-playbook [play book name] --ask-vault-pass`  

## Using a password file and rekeying  
`ansible-playbook [playbook] --vault-password-file=~/.vault`  
`ansible-vault --vault-password-file=~/.[file name] create vault/[file name]`  
`ansible-vault rekey vault/api_keys`  
`ansible-vault view vault/[file name] --vault-password-file=~/.vault`  
**REDO SECTION**


## Vault 1, 2, and multiple Vault IDs
**REDO SECTION**  

## Changing Vault IDs and Encrypting Strings in files
**REDO SECTION**  

## Encrypting mysql password with Vault
**REDO SECTION**  
