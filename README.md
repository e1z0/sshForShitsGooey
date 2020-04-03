sshForShitsGooey
================

GUI for https://github.com/e1z0/sshForShits

Install
================
Install nodejs at least 6.x version on your server
```
git clone https://github.com/e1z0/sshForShitsGooey.git
cd sshForShitsGooey
(root) npm install --global gulp-cli node-gyp
npm cache clean && rm -rf node_modules && npm install
cd node_modules/mongo
npm install
```

Edit file file lib/db/db.js
comment out these lines:
```
var dbcreds = require('./dbcreds.json');
var connectString = 'mongodb://' + dbcreds.username + ':' + dbcreds.password + '@ds063140.mongolab.com:63140/sshforshits';
```
Add line after these lines (it should contain valid user/password for your mongo database):
```
var connectString = 'mongodb://sshforshits:password@127.0.0.1:27017/sshforshits';
```

Run the whole thing:
```
nodejs server.js
```

I've provide you with the systemd service unit for automate the startup operation (sshForShitsGui.service):
```
[Unit]
Description=sshForShitsGooey
After=network-online.target
Wants=network-online.target

[Service]
Type=Simple
User=<username>
Group=<username>
WorkingDirectory=/<path_to_script_directory>/sshForShitsGooey
ExecStart=/usr/bin/nodejs /home/<path_to_script_directory/sshForShitsGooey/server.js
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Do not pay attention to this error
```
Error: Cannot find module 'mongodb/node_modules/bson'
```
