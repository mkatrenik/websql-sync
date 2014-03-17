websql-sync
===========

sync local websql with remote endpoint
 - minimal
 - handles deletes

```js
var sync = websqlSync({
  db: openDatabase('test', '0.1', 'Test DB', 5*1024*1024),
  tableName: 'todos',
  url: '/api/todos',
  id: 'uuid' //custom id field name
});
```

then you need to init db tables and triggers used by websql-sync
```js
// init this modules tables (_events, _lastSync)
sync.init(function(){ 
  // create your db table which you want to sync
  websqlSync.orm.query('CREATE TABLE IF NOT EXISTS todos ' +
    '(id TEXT PRIMARY KEY, value TEXT)', null, function(err, res){
    // init modules triggers
    sync.initTriggers(function(){});
  });
});
```

and finally sync with remote endpoint
```js
sync.sync(function(err, res, tx){});
```