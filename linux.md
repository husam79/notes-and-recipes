## Linux Commands
- sudo usermod -a -G examplegroup exampleusername //adding an exampleusername to a group: examplegroup
- rm -rf dir1 //to remove a directory with all content inside it

# Copy files from current machine to remote machine (ssh)
```
scp -i [pem file if exists] [src_file] [user]@[remote_server_address]:[dest_file_location_with_filename] 
```

Example:
```
scp -i ledger-app-vm_key.pem ./about.png husam@id_address:~/about.png


