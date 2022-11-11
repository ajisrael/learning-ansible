# Generate SSH Keys

## SSH Directory Path
List ssh directory
```
ls ~/.ssh/authorized_keys
```

## Generate Keys
Command to generate a new set of keys (run on local computer)
```
ssh-keygen -t rsa
```
Default path and empty passphrase is fine for lab purposes

## Copy New Key To Remote Server
Command to copy new key ```id_rsa.pub``` to new server
```
ssh-copy-id -i ~/.ssh/id_rsa.pub {user_name}@{host_name_or_ip_address}
```
Enter in the password for ```user_name``` and the key should be added. Just try to ssh into the remote server to verify that it worked.