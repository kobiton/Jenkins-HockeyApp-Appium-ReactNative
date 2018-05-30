# 2. Running automation test with Kobiton

## 2.1 Preriquisites

* Username
* API key
* Desired cap

## 2.2 Setup Jenkins

Show how to setup Jenkins to run automation testing

### 2.2.1 For Jenkins Freestyle

### 2.2.2 For Jenkins Pipeline

## 2.3 Running automation testing

### 2.3.1 Test scripts

* How to write a simple test
* How to run that test script

### 2.3.2 Output

#### Success case

Get all information we can get through public api

**1. Session information**

How to get these information:

* Session name
* Session description
* Device orientation
* Device name
* Platform name
* App
* Kobiton session id

**2. Test logs**

Remember to prepare basic authentication

How to get these information:

* App version
* Logs url 
* Video url
* Commands

> Noted: We will have a lot of commands, so we need to show them how to get the other commands through api.

**3. Final result**

That test is successful or failed

#### Failure case

* Device is already booked (select another device)
* Other (get support from Kobiton)