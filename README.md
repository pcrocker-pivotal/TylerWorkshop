# TylerWorkshop

## Introduction

Use this tutorial to get a sample app up and running on Pivotal Cloud Foundry (PCF). In this workshop we will be using a dedicated instance of PCF hosted by Pivotal.

## Install the CF CLI

Download and install the Cloud Foundry Command Line Interface (cf CLI):

- https://github.com/cloudfoundry/cli/releases

Try the following command to test that the cf CLI works:

`cf help`

You can use the cf CLI to perform all commands on apps deployed to PCF.

## Deploy the Sample App

Now that you have the cf CLI installed, you are really close to deploying the sample .NET app.

Download the app with git:

`git clone https://github.com/Pivotal-Field-Engineering/pcf-dotnet-environment-viewer.git`

If you don't have Git installed, you can download a zip file of the app at https://github.com/Pivotal-Field-Engineering/pcf-dotnet-environment-viewer/archive/master.zip

Navigate to the app directory:

`cd pcf-dotnet-environment-viewer`

Change into the environment folder that holds the app code:

`cd ViewEnvironment`

Sign in to Pivotal Cloud Foundry:

`cf login -a api.run.haas-120.pez.pivotal.io --skip-ssl-validation`

Push the app to PWS:

`cf push`

In the push summary, find the url for the application and open the sample app in your browser.

## View the Logs

View a snapshot of recent logs:

`cf logs env --recent`

Or, stream live logs:

`cf logs env`

PCF provides access to an aggregated view of logs related to your application. This includes HTTP access logs, as well as output from app operations such as scaling, restarting, and restaging.

Every log line contains four fields:

- Timestamp
- Log type
- Channel
- Message
- cf CLI log fields

Press Control C to stop streaming.

## Connect a Database

PCF enables administrators to provide a variety of services on the platform that can easily be consumed by applications.

List the available MySQL plans:

`cf marketplace -s p-mysql`

Create a service instance with the default plan:

`cf create-service p-mysql 100mb env-db`

Bind the newly created service to the app:

`cf bind-service env env-db`

Once a service is bound to an app, environment variables are stored that allow the app to connect to the service after a push, restage, or restart command.

Restart the app:

`cf restart env`

Verify the new service is bound to the app:

`cf services`

## Scale the App

Increasing the available disk space or memory can improve overall app performance. Similarly, running additional instances of an app can allow an app to handle increases in user load and concurrent requests. These adjustments are called scaling.

Scaling your app horizontally adds or removes app instances. Adding more instances allows your application to handle increased traffic and demand.

![Horizontal scaling](https://d1fto35gcfffzn.cloudfront.net/images/products/gettingstartedwithpcf/scaling@2x.png)

Horizontal scaling increases the number of app instances to handle increased demand.
Increase the number of app instances from one to two:

`cf scale env -i 2`

Check the status of the app and verify there are two instances running:

`cf app env`

Scaling your app vertically changes the disk space limit or memory limit for each app instance.

Increase the memory limit for each app instance:

`cf scale env -m 1G`

Increase the disk limit for each app instance:

`cf scale env -k 2G`

## Next Steps

Nice work! You have just deployed and scaled an app with PCF!

Topics to explore:
How PCF Works 
https://docs.pivotal.io/pivotalcf/concepts

PCF Documentation 
https://docs.pivotal.io/pivotalcf/installing/pcf-docs.html

Installing PCF (IaaS-specific guides for installing PCF) 
https://docs.pivotal.io/pivotalcf/installing/

Explore and download more Cloud Foundry sample apps 
https://github.com/cloudfoundry-samples/

Enroll in Pivotal Cloud Foundry Developer Training 
https://pivotal.io/training/courses/pivotal-cloud-foundry-developer-training
