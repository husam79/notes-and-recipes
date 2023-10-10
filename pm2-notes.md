# PM2 Notes

npm install pm2@latest -g

## IMPORTANT

Ensure when you use the pm2 start command to execute it in the same location as the .env file is.

For example if the .env in the current folder, but the app.js file in the dist folder (dist folder in the current folder) then you can execute the current command:
```
pm2 start ./dist/app.js --name [new-app-name]
```
This will ensure that the application that is in the app.js will find the .env file.

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
