[![Gitter](https://badges.gitter.im/watchit-app/community.svg)](https://gitter.im/watchit-app/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)


# watchit-gateway
Gateway Watchit Seeder

## How

*Start docker containers*

1) `docker-compose up`

*Migrate movies to mongodb (Please wait until movies get ready migrated)*

2) `docker-compose exec watchit_migrator bash -c "export PYTHONPATH=$PYTHONPATH:/data/watchit && python resource/py/migrate.py"`

*Initialize IPFS*

3) `ipfs init`

*In a new console please get ID and copy it*

4) `ipfs id # Copy ipfs ID (ex: QmNWCiQTM1drWrdAM5jgRjdGiDoy7sYjznpip1BZU1Jz5m)`

*Now lets get init and set bootstrap ipfs node*

5) `bash ./resource/bash/init_ipfs.sh {YOUR_IPFS_ID_HERE}`

*Run ipfs daemon as background*

6) `ipfs daemon  --enable-pubsub-experiment &`

*And expose our node tu ipfs network over orbitdb migration*

7) `bash ./resource/bash/restart_ipfs.sh`


# watchit-app

*After run migration (Step 2) and expose our node in gateway (Step 7)*

1) Two file are generated `hash` and `clients`. Please copy first entry hash in `hash (Private Key)` file and any of the list in `clients (Public Key)` file. This keys will be requested on app login. 

*To configure your app please*

2) In [this file](https://github.com/ZorrillosDev/watchit-desktop/blob/master/public/lib/settings/orbit.js) set your ENV variables with: `BOOTSTRAP_IP = {GATEWAY_IP} BOOTSTRAP_HASH = {COPIED_ID}`



