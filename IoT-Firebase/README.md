# IoT using Firebase

Being a Microsoft student partner, I am not particularly proud of this workshop but I think it is a good tool for rapid prototyping, something you can use for hackathons. I'll post an Azure version of this soon. Till then, please bear with the GCP version in this tutorial.

I assume you are already familiar with python and are looking for a function or an [API](https://www.infoworld.com/article/3269878/what-is-an-api-application-programming-interfaces-explained.html) which can let you send data to a secured server and receive it from another edge device.
That's all we are going to cover, because you've got many other things to do to win that hackathoms.

## Create an Account

Creating a Firebase account is simple. You can register using an existing Google account [here](https://firebase.google.com/)

Before we can connect to our Firebase database with Python, we need to download a couple of helper modules. We are going to use pip to install them.

      curl https://bootstrap.pypa.io/get-pip.py | python

## Install Pyrebase

Pyrebase is a Python interface to Firebase’s REST API. 
In layman’s terms, it allows you to use Python to manipulate your Firebase database. We will install the Pyrebase and its dependencies using pip. I hope you can intall this on your own without having to refer this for the pip install Pyrebase command.

## Connecting to Database:

Yes, I won't let you type much code, welcome to opensource. Just paste this to connect this to the database/


    import pyrebase
    config = {
    "apiKey": "apiKey",
    "authDomain": "projectId.firebaseapp.com",
    "databaseURL": "https://databaseName.firebaseio.com",
    "storageBucket": "projectId.appspot.com",
     "serviceAccount": "path/to/serviceAccountCredentials.json"
    }
    firebase = pyrebase.initialize_app(config)

## Authentiaction

The default permissions of a Firebase database requires authentication to perform read or write actions. The simplest way to authenticate is by signing in with an email and password. A new user can be created in the Auth tab of the Firebase console. Once a user is created, the following Pyrebase code can be used to created an authentication connection:

    auth = firebase.auth()
    #authenticate a user
    user = auth.sign_in_with_email_and_password("william@hackbrightacademy.com", mySuperStrongPassword")

## CRUD-dy Behavior

Given a table what all actions van be done? Create, read, update and delete. Let's explore how we can do that

### Create


#### Push method: 

    archer = {"name": "Sterling Archer", "agency": "Figgis Agency"}
    db.child("agents").push(archer, user['idToken'])

#### Set method:
    lana = {"name": "Lana Kane", "agency": "Figgis Agency"}
    db.child("agents").child("Lana").set(lana, user['idToken'])

### Read 

#### You can get all of the values of an object
  
      all_agents = db.child("agents").get(user['idToken']).val()

#### Or you can get a specific value of an object

      lana_data = db.child("agents").child("Lana").get(user['idToken']).val()

### Update

Updates can be made with the let's guess, 
.
.
update() method.

    db.child("agents").child("Lana").update({"name": "Lana Anthony Kane"}, user['idToken'])

### Delete 
##### just what google should do for majority of it's services (No Offence, everyone is entitled to their faith and cloud services)

The remove() method removes objects from the database. 
    
    db.child("agents").remove(user['idToken'])

Or a specific value from an object
    
    db.child("agents").child("Lana").remove(user['idToken'])


### That's it! Congratulations, I hope you got it done, If not, you know [where](https://medium.com/@scosta/why-firebase-sucks-ce5d2302eb20) to go
### Happy Hacking!
