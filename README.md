# Connect Session Store using Sequelize

connect-session-sequelize is a SQL session store using [Sequelize.js](http://sequelizejs.com).

#IMPORTANT

**NOTE this project is really just a fork renamed (consistent with connect-mongo, connect-redis etc.) along with the added feature of being able to define the Session table name within your SQL database.

Thanks to [Michael Weibel](https://github.com/mweibel) for the awesome work!!!

# Installation
Please note that the most recent version requires **express 4.** If you use *express 3* you should install version 0.0.5 and follow [the instructions in the previous README](https://github.com/mweibel/connect-session-sequelize/blob/7a446de5a7a2ebc562d288a22896d55f0fbe6e5d/README.md).

```
$ npm install connect-session-sequelize
```

# Options

* `db` a successfully connected Sequelize instance

# Usage

With connect

```javascript
var connect = require('connect')
	// for express, just call it with 'require('express-session').Store'
	, SequelizeStore = require('connect-session-sequelize')(connect.session.Store);

connect().use(connect.session({
	store: new SequelizeStore(options)
	, secret: 'CHANGEME'
}));
```

With express 4:

```javascript

// load dependencies
var express = require('express')
var Sequelize = require('sequelize')
var cookieParser = require('cookie-parser')
var session = require('express-session');

// initalize sequelize with session store
var SequelizeStore = require('connect-session-sequelize')(session.Store);

// create database, ensure 'sqlite3' in your package.json
var sequelize = new Sequelize(
"database",
"username",
"password", {
    "dialect": "sqlite",
    "storage": "./session.sqlite",
    "table": "Session"
});

// configure express
var app = express()
app.use(cookieParser())
app.use(session({
  secret: 'keyboard cat',
  store: new SequelizeStore({
    db: sequelize
  }),
  proxy: true // if you do SSL outside of node.
}))
// continue as normal
```


# License

MIT
