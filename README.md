sonos-api-nocode
======================

# About

Source for a nodejs no-code flow-based palette for Sonos APIs. API Code and Token generator tools and sample applications included. Built in pub-sub data broker to connect event-based programming with Sonos API actions. 

repo is synced with docker hub at brianapley/sonos-api-nocode.

## Launching via docker (example)

```
docker run -it -p 1880:1880 -v nrdata:/data --name sonos-api-nocode brianapley/sonos-api-nocode
```

Once launched, UI can be accessed via http://host:1880/ui. The node-RED pallete can be accessed via http://host:1880/. 

# How to Use

From the UI URL, there are two tabs, Auth API and Control API. Use the top left menu button to navigate between them.

## Initial Authentication

Navigate to the Auth API tab for the intial authentication. 

<img width="794" alt="image" src="https://user-images.githubusercontent.com/19197357/194899356-71fe902b-35b3-4348-8a02-4b897ac9d9b7.png">

1. From the Auth API, first enter a unique value for "State" in the top form field and hit "submit." The text below the form should update with the login URL (you should see your "state" entered as a query string argument).

<img width="796" alt="image" src="https://user-images.githubusercontent.com/19197357/194899714-7a3b4833-ce2a-40bb-92ff-ae2de81be111.png">

2. Copy that login URL value and load it into a new browser window. You'll be prompted to login to Sonos, and will be asked to give permission to the Linode Workshop Integration to control your system. 

<img width="785" alt="image" src="https://user-images.githubusercontent.com/19197357/194882354-9b14dd56-712a-4554-9667-4f4d090ac30f.png">

3. Once permission is granted, your browser will be redirected to a page that shows a json with your state and code value. Copy the code value for the next step.

```
{"state":"{state value}","code":"{code value"}
```

4. Navigate back to the sonos-api-nocode UI, and paste the code value into the form on step 2. Hit "Submit," and a Sonos API token will be retrieved, and loaded into the application.

<img width="1068" alt="image" src="https://user-images.githubusercontent.com/19197357/194895687-5a41e5c8-287a-4a80-92c1-0b148996c011.png">


NOTE- the token expires after 24 hours, and there is no refresh routine at present.

## Using the Control UI

Once an authentication token is loaded, the Control UI can be used to execute some basic Sonos APIs, and explore possible service integrations. Navigate to the Control UI table via the top left menu.

<img width="579" alt="image" src="https://user-images.githubusercontent.com/19197357/194901720-18e1b8e6-430f-4d40-a0c0-80453720c806.png">

Select "Get Households, Groups, and Players" - This loads objects from the Sonos Cloud API for discovering information about controlled Sonos system. The left table should populate with a list of group names and their ID.

<img width="302" alt="image" src="https://user-images.githubusercontent.com/19197357/194902349-cfcd4504-8a8d-49c0-b12e-dcd40a67b591.png">

Selecting an entry in the table will populate that ID value of the group loads into the "Send Command" and "What's Playing" services. 

Submitting the ID in the "What's Playing" form will populate the below table with the artist, track, and album of the currently playing track in that group. Selecting that track table entry will then make an API call to genius.com, and return the first playlist art object returned in the search.

![image](https://user-images.githubusercontent.com/19197357/194904413-ca7fe10a-9990-442d-8ad6-d4a745580089.jpeg)

The "Send Command" form can be used to send POST API commands to group IDs. A "type" value (such as playback), and an "action" value (such as play or pause) can be sent.

<img width="265" alt="image" src="https://user-images.githubusercontent.com/19197357/194905180-89499483-4065-48df-aec8-7aebf9fad8ff.png">

## Using the node-RED pallette to design services and integrations

The node-RED pallette can be accessed via the root of the service- i.e., http://host:1880/.

<img width="1366" alt="image" src="https://user-images.githubusercontent.com/19197357/194905474-b22764c1-f8ab-476d-8ea0-3f14cb476cc8.png">

Within the node-RED pallette, tabs can be seen for the Auth and Control API services 
