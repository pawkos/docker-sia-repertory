# docker-sia

[![Build Status](https://travis-ci.org/mtlynch/docker-sia.svg?branch=master)](https://travis-ci.org/mtlynch/docker-sia)
[![Docker Automated build](https://img.shields.io/docker/automated/mtlynch/sia.svg?maxAge=2592000)](https://hub.docker.com/r/mtlynch/sia/)
[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](LICENSE)

## Usage

```bash
mkdir sia-data
docker run \
  --detach \
  --volume $(pwd)/sia-data:/sia-data \
  --publish 127.0.0.1:9980:9980 \
  --publish 9981:9981 \
  --publish 9982:9982 \
  --name sia-container \
   mtlynch/sia
```

**Important**: Never publish port 9980 to all interfaces. This is a security-sensitive API, so only expose it beyond 127.0.0.1 if you know what you're doing.

Once the container is running, you can execute siac from within the container:

```bash
$ docker exec -it sia-container ./siac consensus
Synced: No
Height: 3800
Progress (estimated): 2.4%
```

You can also call siad from outside the container:

```bash
$ curl -A "Sia-Agent" "http://localhost:9980/consensus"
{"synced":false,"height":4690,"currentblock":"0000000000007d656e3bb0099737892b9073259cb05883b04c6f518fbf0faffb","target":[0,0,0,0,0,2,200,179,126,85,220,153,25,190,195,228,72,53,129,181,62,124,175,60,255,90,105,68,179,16,6,71],"difficulty":"101104922300609"}
```
