# 2. Running automation test with Kobiton

#### 2.1 Prepare Kobiton configuration for executing automation testing

* #### Username 
1. Go to https://portal.kobiton.com/
2. In the upper right hand corner, click on your name and in the drop down menu, click on Profile. 

![profile](assets/2-profile-user.png)

3. You should see the username. 

![username](assets/2-username.png)

* #### API key
1. Click on your name in the upper righthand corner again and select settings. 
2. You should be able to find your API key under 'API Keys'. 

![api-key](assets/2-apikey.png)

* #### Desired cap
1. In the navigation bar at the top of the Kobiton website, select Devices. 
2. Hover over any device and click on the Automation settings button (the gear symbol). 

![automation](assets/2-automation.png)

3. On the left hand side, you can select your preferred language, as well as any other variables you would like to adjust, such as **App Type**, **Device Group**, and **Orientation**. Adjusting the settings on the left side will affect the desiredCaps, which you can find in the right side of the window. 

![automation-settings](assets/2-automationsettings.png)

## 2.2 Create new Jenkins project to execute the automation test

#### How to setup Jenkins to run automation testing

Jenkins is an open source automation server that provides hundreds of plugins to support building, deploying, and automating any project. 

Download Jenkins from https://jenkins.io/ and make sure you have a Jenkins server available with a public domain. 

**2.2.1 Write the automation test script**

* How to write a simple test

For examples of automation tests, go to https://github.com/kobiton/samples . 

Choose a language for your test script, and decide whether you want to test on Android or iOS, and either do a web test or an app test. Make sure in the code you specify your Kobiton username, API key, and information under desiredCaps. 

**2.2.2 Create Jenkins project**

On the left side on the page, click on New Item to start a new Jenkins project. 

![new-item](assets/2-new-item.png)

Enter in a name for the project and select 'Freestyle project'. Hit 'OK'. 

![project](assets/2-project.png)

Go to Configure in your Jenkins project. Add a build step, execute shell. 

![build-execute-shell](assets/2-build-execute-shell.png)

Enter this in the command. Enter your own Kobiton  username and API key as well as the desired device and platform you wish to test with. The below example will execute the android-web-test script sample from Kobiton. 
```
#!/bin/bash
[ ! -d "samples" ] && git clone https://github.com/kobiton/samples.git || echo "Samples already exist"
cd samples/javascript
npm install
KOBITON_API_KEY=... KOBITON_USERNAME=... npm run android-web-test
```

This guide is executing the NodeJS test script from the Kobiton samples, so we will add the NodeJS Plugin on Jenkins to execute NodeJS script as a build step. To do this, go to 'Manage Jenkins' -> 'Manage Plugins' -> Available. Search for NodeJS and install it.

![manage-plugins](assets/2-manageplugins.png)

If you are using a different language, you may try to find a suitable plugin for your project if necessary.

Under build environment, check the box that says 'Provide Node & npm bin/ folder to PATH'.

![build-environment](assets/2-build-environment.png)

**2.2.3 Trigger Jenkins project by pushing on GitHub**

Try Build now and check Kobiton cloud devices to see if a test session was created. 

**2.2.4 Get the automation session data through Kobiton REST API**


- Update test result to session (https://api.kobiton.com/docs/#update-session-information)

```
PUT /sessions/{sessionId}
``` 
To make a request:

1. Encode your credential in base64 for HTTP Basic Authentication, you may use below command and note the text result

```
echo -n <your username>:<your api-key> | base64
```
2. Use encoded base64 from above in curl commands, like below

```
curl -X GET https://api.kobiton.com/v1/sessions \
  -H 'Authorization: Basic dGVzdHVzZXI6MTIzZWQtMTIzZmFjLTkxMzdkY2E='
  -H 'Accept: application/json'
```

Below are necessary Kobiton Rest API endpoints that you may need.

- Get session info
```
GET /sessions{sessionId}
```
To make a request:
```
curl -X GET https://api.kobiton.com/v1/sessions/{sessionId} \
  -H 'Authorization: Basic dGVzdHVzZXI6MTIzZWQtMTIzZmFjLTkxMzdkY2E='
  -H 'Accept: application/json'
```

With this line of code, you can print the session information to the console. 
```javascript
console.log(sessionCapabilities)
```

- Get session commands
```
GET /sessions/{sessionId}/commands
```
To make a request:

```Shell
curl -X GET https://api.kobiton.com/v1/sessions/{sessionId}/commands \
  -H 'Authorization: Basic dGVzdHVzZXI6MTIzZWQtMTIzZmFjLTkxMzdkY2E='
  -H 'Accept: application/json'

```
To get to a certain page in your commands, add the page number to the commands URL. For example:
```javascript
`https://api-test.kobiton.com/v1/sessions/${sessionId}/commands?page=2`
```

> For more details on how to retrieve information about your session, go to https://api.kobiton.com/docs/

## Final result

The test is a either a success or failure.

#### Failure case

* Error: "The environment you requested was unavailable." 
    - This means that the device you selected is already booked. Either select a different device or wait a few moments until your device becomes available
* Other 
    - Contact Kobiton for support
    - Go to portal.kobiton.com
    - In the navigation bar at the top of the page, click on 'Support'

    ![support](assets/2-support.png)

    - Fill in the information for your request and submit your ticket

    ![submit-ticket](assets/2-submit-ticket.png)
