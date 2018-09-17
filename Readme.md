# Problems I faced
## Connecting to the Eureka Service provided by PCF
I had some issues here where I could not get it to connect ... And then I found out there was a different dependency that I needed to include that is not the normal eureka dependency  
## Communicating with Account Service from Zuul
Apparently don't use Edgeware.RELEASE for your gateway service. It will connect to the Service Registry but then will not properly forward the requests to the account service ... something to do with HTTPS in that version.

# Status of this Repo
## Currently Working
* The account service will deploy and connect to the provided Service Registry on pcf.
* The gateway service will deploy and connect to the provided Service Registry on pcf and will route to the account service.

## ToDo
* Haven't tried the customer service but it should work fine.
* Clean up gateway service application.yml since I tried multiple things trying to get it to work that I don't believe I need.
* Example with the RabbitMQ instance provided by PCF
* Step by step notes
* Add more notes for studying


# Study
## What is cloud Foundry?
Cloud Foundry is an open source standard for PaaS which allows you to deploy applications to any cloud computing service. You could also run CF on your own infrastructure. 

## What is pcf?
PCF (Pivotal Cloud Foundry) is a commercial version of CF that provides some additional third party services for developers to interact with. 

Pivotal Web Services is Cloud Foundry hosted by Pivotal where you do not have to manage the infrastructure and cloudfoundry installation.

## Buildpacks
Pretty much the way it works is you push your app to PCF and it will scan your code to automatically detect which build pack it needs to use. The buildpack provides the runtime needed to run your application. For the most part you are fine just using the buildpacks already registered with PCF but if you need you can also create custom buildpacks.

[Official Documentation](https://docs.cloudfoundry.org/buildpacks/)

## Manifest.yml
A manifest is not required, however it is suggested that you use one because it will provide consistency in how your application is deployed to different clouds. The manifest can specify things such as
 * What is the name of the application.
 * How many instances of the app you want deployed
 * How much memory you want each instance to have
 * Custom buildpacks
 * Docker images to run on
 * Routing
 * Path to your application 
 * Environment variables
 * and more

 [Official Documentation](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html)

## Routes AND Domains
If you do not specify any routing information when pushingt to pcf it will try to create a route based on the application name, you can also set it to random route if you are trying to deploy the route in multiple spaces or you can turn routing off if the app you are deploying is more for just running background processes. 

You can also manually create routes and assign apps to routes. When creating routes you have to specify which domain you want to use. PCF will provide you with a few domains to use initially but you can also register your own Domain by linking your DNS provider. For more information on this refer to their [Official Documentation](https://docs.cloudfoundry.org/devguide/deploy-apps/routes-domains.html)


## Droplets

