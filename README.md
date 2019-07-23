# pouch-sync-gateway-couchbase-example
Example project about sync between pouchDb and Couchbase 5.1 

Based on article "Introduction to offline data storage and sync with PouchBD and Couchbase" https://blog.couchbase.com/introduction-offline-data-storage-sync-pouchdb-couchbase/  

You will need docker, node + npm and optionally python.

 1.Run Couchbase Server in docker:
```
docker run -d --name couchbase -p 8091-8094:8091-8094 -p 11210:11210 couchbase
```
 2. Go to http://localhost:8091 and create bucket with name "default" and user "sync_gateway" with pass "sync_gateway" and roles Bucket Full Access[*], Read Only Admin

 3. Run Couchbase Sync Gateway and give properties through volume (replace /path/to/config/dir to actual path where you put config.json for sync-gateway:
```
docker run -p 4984:4984 --name sync-gateway -d -v /path/to/config/dir:/tmp/config couchbase/sync-gateway /tmp/config/config.json
```
 4. In directory with index.html you need to run http server on port 8888 so CORS check will work. You can run it with python 3 as:
```
python -m http.server 8888
```

 5. Go to http://localhost:8888 and check synchronization between indexDb and Couchbase
