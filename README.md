election-result-demo
======================

### About

Source for a docker container for a node-red based MQTT Election result demo.

repo is synced with docker hub at brianapley/election-result-demo.

## Launching via docker hub (example)

```
docker run -it -p 1880:1880 -v nrdata:/data --name node-red-election-result brianapley/election-result-demo
```

Once launched, UI can be accessed via http://host:1880/.

