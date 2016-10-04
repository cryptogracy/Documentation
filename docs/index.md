
Welcome to SharedSecret Docs
============================

RESTful API
-----------

- `GET /`
    - Upload UI
    - Serve `/ui/upload.html`
    - 200 OK
- `GET /ui/*`
    - Ressources
    - Serve static file
    - 200 OK
    - 404 NOT FOUND
- `PUT /api/files/<hash>`
    - → `enc(part)`
    - → `x-file-lifespan` (minutes:int)
    - 201 CREATED
    - 409 CONFLICT
- `GET /api/files/<hash>`
    - Returns: File
    - 200 OK
    - 404 NOT FOUND
- `GET /<hash>`
    - Download UI
    - Serve `/ui/download.html`
    - 200 OK
- `PUSH /api/metadata`
    - → `enc([hash_part_1, hash_part_2, …])`
    - → `x-file-lifespan` (minutes:int)
    - ← `<id>`
    - 201 CREATED
    - 400 BAD REQUEST
- `GET /api/metadata/<id>`
    - ← `enc([hash_part_1, hash_part_2, …])`
    - 200 OK
    - 404 NOT FOUND


### Example API Calls

Upload:

```
for hash(part) in parts:
    PUT /api/files/<hash>
        -> enc(part)
        <- 201 CREATED

PUSH /api/metadata
    -> enc([hash_part_1, hash_part_2, …])
    -> x-file-lifespan (minutes:int)
    <- 201 CREATED
    <- <id>
```

Download:

```
GET /api/metadata/<id>
    200 OK
    <- enc([hash_part_1, hash_part_2, …])

for hash in metadata:
    GET /api/files/<hash>
        200 OK
        <- enc(part)
```


User Interface
--------------

- Before Upload:
    - lifespan (dropdown)
    - password [generator]
    - browse file
    - Upload button
- After Upload:
    - Download link
- Download
    - Password
    - Download button
