** PM2 Notes

IMPORTANT: 

Ensure when you use the pm2 start command to execute it in the same location as the .env file is.

For example if the .env in the current folder, but the app.js file in the dist folder (dist folder in the current folder) then you can execute the current command:
```
pm2 start ./dist/app.js
```
This will ensure that the application that is in the app.js will find the .env file.
