# accountdown-model

This module is a wrapper around accountdown that provides a few extra features: changing username & password, validation using json-schema, and simple indexing of properties.

It's meant to have roughly the same api & features as [level-model](http://npmjs.org/level-model)

## Installation

```
npm install --save accountdown-model
```

## Usage

Currently you must use [accountdown-basic](http://npmjs.org/accountdown-basic) and you must use `key` as the name of the identifier for the account. You also must pass the level db as an option. Basically, you'll want to set up the modules exactly like this:

```
var db = level('example')

function accountdownBasic (db, prefix) {
  return require('accountdown-basic')(db, prefix, { key: 'key' })
}

var accountdown = accountdown(sublevel(db, 'accounts'), {
  login: { basic: accountdownBasic }
})

var accounts = require('accountdown-model')(accountdown, { 
  db: db
})
```

Additionally, you can specify properties that should be stored in the `value` object of the account, and control which of those properties should be required and indexed.

An example:

```
var accounts = require('accountdown-basic')(accountdown, { 
  db: db,
  properties: {
    username: { type: 'string' },
    email: { type: 'string' }
  },
  required: ['username', 'email'],
  indexKeys: ['username', 'email']
})
```

## API

Exactly the same as [accountdown](http://npmjs.org/accountdown), with these additions:

```
var accounts = require('accountdown-model')(accountdown, { 
  db: db
})
```

### `accounts.update(key, data, callback)`

Updates the indexes of the properties and saves the values.

### `accounts.changePassword(key, password, callback)`

### `accounts.changeUsername(key, username, callback)`

## License

MIT