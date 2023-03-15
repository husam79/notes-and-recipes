# Linux Commands

## Adding an exampleusername to a group: examplegroup
```
sudo usermod -a -G examplegroup exampleusername 
```

## Removing a folder with all contents inside it
```
rm -rf dir1
```

## Copy files from current machine to remote machine (ssh)
```
scp -i [pem file if exists] [src_file] [user]@[remote_server_address]:[dest_file_location_with_filename] 
```

Example:
```
scp -i ledger-app-vm_key.pem ./about.png husam@id_address:~/about.png
```

Note: If the authentication method to a server is by using a password (instead of a key) then this command will prompt you to enter username and password as you used to do in normal ssh client.
