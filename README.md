sonos-api-nocode
======================

### About

Source for a nodejs no-code flow-based palette for Sonos APIs. API Code and Token generator tools and sample applications included. Built in pub-sub data broker to connect event-based programming with Sonos API actions. 

repo is synced with docker hub at brianapley/sonos-api-nocode.

## Launching via docker (example)

```
docker run -it -p 1880:1880 -v nrdata:/data --name sonos-api-nocode brianapley/sonos-api-nocode
```

Once launched, UI can be accessed via http://host:1880/.

