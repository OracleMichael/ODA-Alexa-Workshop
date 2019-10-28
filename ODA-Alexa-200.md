# ODA-Alexa Integration - Heroku Node Server Setup

Updated: October 25th, 2019

This part of the lab builds the backend server to be hosted on Heroku. The backend server uses Node JS and effectively sits between Alexa and Digital Assistant, translating each other's output into input recognized by the other.

## Objectives
- Create Heroku account
- Set up Heroku on local computer
- Create a Heroku Application
- Configure webhooks
  - Update Digital Assistant channel URL
  - Update Amazon endpoint
- Configure and deploy Node JS server
  - Update Amazon AppID
  - Update Channel Secret Key and Channel URL
  - Modify `package.json`
- Test the application

## Required Artifacts
- Oracle Digital Assistant Skill
- Heroku Account
- **Download the Node JS code [here](https://app.compendium.com/api/post\_attachments/32ab85fd-0f44-4856-a79f-91a61359717b/view)** and unzip the zip file. The code has the following structure:

```
MyAlexaWebhook
  index.js
  invocation.json
  package.json
  README.md
  server.js
```

# Create Heroku Account

Follow this [link](https://signup.heroku.com/?c=70130000001xDpdAAE&gclid=Cj0KCQjwuZDtBRDvARIsAPXFx3DyRB323ksXfO_lYs7W14RB6CRCTQjMBNQTOuElUazr4rbuGysu78waAvLDEALw_wcB) to create a Heroku account. 

# Set up Heroku on local computer

Follow this [link](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up) to set up Heroku on a local computer. For macOS, either the brew command or the download will install Heroku. To check on macOS, open a terminal (press command+space and search "terminal") and run `command -v heroku`. If you see something along the lines of `/usr/.../heroku` then heroku is installed.

# Heroku application deployment setup

## Follow the below steps to create an app in heroku and deploy the sample code.

### **STEP 1**: Go to Heroku dashboard and create an app

- Click **New** and then **Create new app**.

  ![](images/200heroku/createApp.png)  

- You may optionally enter a unique app name. If you choose not to, Heroku will generate one for you.
  **OR**
  Create an app from the [command line interface](https://devcenter.heroku.com/articles/creating-apps).

  ![](images/200heroku/appName.png)

### **STEP 2**: Initialize server directory

- In your terminal (macOS/linux: terminal; windows: install git bash), go **INTO** the directory you downloaded. Make sure the downloaded zip file is unzipped. For instance, if the zip file was downloaded to your downloads folder and unzipped there, run

```
cd Downloads/MyAlexaWebhook
```

- Log into Heroku by running the following command:

```
heroku login
```

- Initialize a Heroku Github repository in `MyAlexaWebhook`. This is for tracking changes you make to the code and for pushing (uploading) your changes to your Heroku server.

```
git init
heroku git: remote -a <INSERT APP NAME>
```

  Remember to replace <INSERT APP NAME> with the Heroku app name from **STEP 1**.

# Configure webhooks

## In this section we will use the Heroku application name to finalize the webhook URLs.

### **STEP 1**: Go to your Oracle Digital Assistant Instance

  ![](images/200heroku/odaInstance.png)

### **STEP 2**: Navigate to the channel you created in lab 050, step 5

- Change the **Outgoing Webhook URI** to `https://HEROKU_SERVER_NAME.herokuapp.com/singleBotWebhook/messages` where `HEROKU_SERVER_NAME` is the name of the Heroku application.

  ![](images/200heroku/createWH.png)

### **STEP 3**: Go to your Alexa Skill

- Click on your skill to open the development console.

  ![](images/200alexa/alexa-endpoint-1.png)

### **STEP 4**: Navigate to endpoints

- Click on "Endpoints" on the left-hand navigation menu.

  <img src="images/200alexa/alexa-endpoint-2.png" alt="" width="200">

### **STEP 5**: Configure the endpoint

- Select HTTPS. Edit the **default region** module.

- The **URL** will be `https://HEROKU_SERVER_NAME.herokuapp.com/alexa/app`.

- Select "My deployment endpoint is a sub-domain of a domain that has a wildcard certificate from a certificate authority".

  <img src="images/200alexa/alexa-endpoint-3.png" alt="" width="80%">
 
# Deploy Node JS application

## Before we redeploy the Node JS application we need to make some changes in `service.js`.

### **STEP 1**: Open `service.js` in a code editor

- You may use VSCode (shown), your favorite Integrated Development Environment (IDE), Notepad, ViM, etc.

  ![](images/200heroku/servicejs.png)

### **STEP 2**: Change amazon application ID in `service.js`

- Use the amazon application id (see lab 100 step 5) and copy it here:

  ![](images/200heroku/appID.png)

### **STEP 3**: Change channelSecretKey in `service.js`

  ![](images/200heroku/channelSecretKey.png)

### **STEP 4**: Change channelUrl in `service.js`

  ![](images/200heroku/channelUrl.png)

### **STEP 5**: Modify `package.json`

- Inside of the server you downloaded there is a file called `package.json`. Replace its contents with the code below. 

```
{
  "name": "oracle-bot-alexa",
  "version": "1.0.0",
  "description": "Alexa integration",
  "main": "service.js",
  "author": "",
  "license": "",
  "dependencies": {
    "@oracle/bots-node-sdk": "2.0.6",
    "alexa-app": "^4.2.0",
    "body-parser": "^1.15.2",
    "express": "^4.14.0",
    "pubsub-js": "^1.5.4",
    "underscore": "^1.8.3",
    "util": "^0.10.3"
  },
  "scripts": {
    "start": "node index.js"
  }
} 
```

### **STEP 5**: Deploy nodeJS application

- Open up terminal and navigate to your directory to where you Node JS server is located. Run these commands:

```
git add .
git commit -am "redeploying with correct variables"
git push heroku master
```

# Test the application

## We will test the application using the Alexa Developer Console.

### **STEP 1**: Test in Alexa Developer Console

- Navigate to your Alexa skill and select the **test** tab. Allow the page to use your microphone, and toggle **Off** to **Development**.

  ![](images/200heroku/testing1.png)

- You will be able to interact with you newly created skill by typing or using your microphone. The format to test is as follow:

```
Alexa, ask [invocation name] [utterance to send to digital assistant skill]
```

- For instance, if your invocation name was "Pizza King" and utterance was "what are my options", you would say:

```
alexa ask pizza king what are my options
```

(Note that punctuation is discarded when talking to the Alexa developer console. 

### **STEP 2**: Example test with the Pizza King bot

- If you hook up the [Pizza King skill](https://github.com/OracleMichael/ODA-Alexa-Workshop/raw/master/PizzaKing.zip) referenced in lab 050 step 4 to the digital assistant channel, you can test out this dialog by either typing in or talking to the Alexa developer console:

  ![](images/200heroku/testing2.png)

**This completes the ODA-Alexa Integration Workshop!**

