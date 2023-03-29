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

## User management in Linux
There are two types of users in linux: normal users and system users. The normal users will have UID of 1000 and above, wherease the system users will have UID below 1000. System users are useful paricularly for cron (automated) jobs.
### Adding a new user
```
sudo useradd -m new_user
```

**Note 1:** If you ommit the -m directive, the user will be created without a home director.
<br />
**Note 2:** If you use the -r directive, with this command, you will create a **system user**.

### Assigning a password for a user
```
sudo passwd some_user
```

Note: you can change your password by executing the `passwd` directly on your command shell.

### Listing all registered users
```
cat /etc/passwd
```
### Removing a user
```
sudo userdel some_user
```

**Note:** If you want to remove the home directory for the some_user you need to add the **-r** directive to the previous command.


