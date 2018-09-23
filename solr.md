# REST API collaboration
[Official documentation for different versions](http://archive.apache.org/dist/lucene/solr/ref-guide/)

**TIP:** *investigate request/response of the Solr UI*

## request types:
* wt=json
* wt=xml


## read collections
```
curl -s localhost:8983/solr/admin/cores?wt=json
```
request to server with https
```
curl -i -k --negotiate -u: https://localhost:8983/solr/admin/cores?wt=json
```
```
curl localhost:8983/solr/admin/collections?action=LIST&wt=json
```

## force commit for core/collection
```
http://localhost:8983/solr/collection1/update?commit=true
```

## insert new record
* xml
```
curl http://localhost:8983/solr/update?commit=true -H "Content-Type: text/xml" --data-binary '<add><doc><field name="id">10010</field><field name="title">title #10010</field></doc></add>'
```

* json simple version
```
curl http://localhost:8983/solr/update?commit=true -H "Content-Type: text/json" --data-binary '[{"id":10011, "title": "title #10011"}]'
```

* json full request
```
curl http://localhost:8983/solr/update?commit=true -H "Content-Type: text/json" --data-binary '{"add":{ "doc":{"id":"1021","title":"title 1021"},"boost":1.0,"overwrite":true,"commitWithin":1}}'
```

* json POST request
```
curl -X POST http://localhost:8983/solr/collection1/update?commit=true -H "Content-Type: text/json" --data '{"add":{ "doc":{"id":"1023","title":"title 1023"},"boost":1.0,"overwrite":true,"commitWithin":1}}'
```

## select records, execute query, read records
* xml
```
curl http://localhost:8983/solr/select?q=*:*
```

* json
```
curl -X GET -H "Accept: application/json, text/javascript" "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true&_=1537470880014"
```

## delete all from collection
```
curl http://localhost:8983/solr/collection1/update?commit=true -H "Content-Type: text/xml" --data-binary '<delete><query>*:*</query></delete>'
```

## delete core/collection itself
```
curl localhost:8985/solr/admin/cores?action=UNLOAD&deleteInstanceDir=true&core=collection1
```

# command line parameters
* -Dsolr.admin.port=8984
SOLR_PORT

* -Dsolr.port=8985
SOLR_ADMIN_PORT

* -Dsolr.solr.home=/var/lib/solr