# Jenkins-HockeyApp-Appium-ReactNative
Guidance on integrating Kobiton service into the build pipeline of mobile app development: Jenkins, HockeyApp, Appium and ReactNative

Let's we're a company or individual that has a mobile application and we have a domain, https://awesome-mapp.com. While developing the app we need to integrate Kobiton into the development and testing pipeline. Here at awesome-mapp, we use: 

- Jenkins to build the app
- HockeyApp for keeping the daily app build

This repo contains guidelines to show how to trigger a Jenkins build from a push on GitHub, and how to run automation tests with Kobiton. 

## Contents
- 1-triggering-jenkins
    - 1.1 Install GitHub Integration Plugin
    - 1.2 Configure GitHub repo to push to Jenkins
    - 1.3 Allow Jenkins to access GitHub repository
- 2-running-automation-testing
    - 2.1 Prepare Kobiton configuration for executing automation testing
    - 2.2 Create new Jenkins project to execute the automation test
        - 2.2.1 Write the automation test script
        - 2.2.2 Create Jenkins project
        - 2.2.3 Trigger Jenkins project by pushing on GitHub
        - 2.2.4 Get the automation session data through Kobiton REST API

