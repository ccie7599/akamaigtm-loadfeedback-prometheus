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

### How to Use

From the UI URL, there are two tabs, Auth API and Control API. Use the top left menu button to navigate between them.

## Initial Authentication

<img width="1181" alt="image" src="https://user-images.githubusercontent.com/19197357/194881058-da5263ea-57e5-4a2e-9efc-9ccaca8ccd5d.png">

1. From the Auth API, first enter a unique value for "State" in the top form field and hit "submit." The text below the form should update with the login URL (you should see your "state" entered as a query string argument).

<img width="1031" alt="image" src="https://user-images.githubusercontent.com/19197357/194881791-5269f128-d261-4a35-8251-96f7b1be0bb0.png">

2. Copy that login URL value and load it into a new browser window. You'll be prompted to login to Sonos, and will be asked to give permission to the Linode Workshop Integration to control your system. 

<img width="785" alt="image" src="https://user-images.githubusercontent.com/19197357/194882354-9b14dd56-712a-4554-9667-4f4d090ac30f.png">

3. Once permission is granted, 

<img width="396" alt="image" src="https://user-images.githubusercontent.com/19197357/194882813-87957a48-79c5-4c1e-9918-a2577190a9cf.png">

