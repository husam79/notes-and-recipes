# PM2 Notes

npm install pm2@latest -g

## IMPORTANT

Ensure when you use the pm2 start command to execute it in the same location as the .env file is.

For example if the .env in the current folder, but the app.js file in the dist folder (dist folder in the current folder) then you can execute the current command:
```
pm2 start ./dist/app.js --name [new-app-name]
```
This will ensure that the application that is in the app.js will find the .env file.

After starting an app, you should sync the pm2 running list by executing the following command:
```
pm2 save
```
This will guarantee running the same apps the next time the system is rebooted.
In case a problem happens and the running list is not synced after rebooting, you can execute the following:
```
pm2 startup
```
you will notice advice from this command to execute another command, execute it, and then execute the following:
```
pm2 save
```
This should fix the problem

# Restart apps
```
pm2 restart all
pm2 restart app-name
```

# Display all apps logs in realtime
```
pm2 logs
```

# Display only `api` application logs
```
pm2 logs api
```

# Display new logs in json
```
pm2 logs --json
```

# Display 1000 lines of api log file
```
pm2 logs big-api --lines 1000
```

# Restart an app with a specific id and rename it in one command
```
pm2 restart [id] --name [new-name]
```
