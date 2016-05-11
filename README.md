# mongo-doc-with-timestamp

## Mongo server side stored javascript.

This stored Server side mongo js iterates over each documents of given collection
and calculate timestamp on the basis of document id (MongoId) and append timestamp to each 
respective document and then, print them.

# How to Use

1. Connect to Mongo Shell.
2. use DB_NAME (Replace DB_NAME with actual db name)
3. Paste the entire js on Mongo Shell (It will store js function on system.js collection and can be reused )

```
db.system.js.save(
   {
     _id: "docsWithTime",
     value : function(collection, query, sort, limit) {
                db[collection].find(query).limit(limit).sort(sort).forEach(function(doc){
                doc.timestamp=doc._id.getTimestamp();
                printjson(doc
            )
      }); 
      }
   }
)
```
4. Load JS.

```
   db.loadServerScripts()
```

5. Issue following command to iterate over a collection where you want timestamp.

```
    docsWithTime('collection_name',{"match":"abc"},{"_id":-1},10)
```

