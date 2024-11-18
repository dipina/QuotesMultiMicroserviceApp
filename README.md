Steps to deploy Quote's 3 microservice app on the Cloud through to Railway platform
===================================================================================
This app would normally be deployed as result of one single "docker-compose up" command. It is an app consisting of 3 microservices:
1) API Gateway microservice
2) Quote microservice which based on a quotes.txt provides quotes from famous people on demand
3) Front end for such microservice

Now, the list of steps carried out to deploy this app over Railway platform are:

0. Visit docs page: https://docs.railway.com/overview/about-railway
Railway is a deployment platform designed to streamline the software development life-cycle, starting with instant deployments and effortless scale, extending to CI/CD integrations and built-in observability.
1. Go to https://railway.app/dashboard
2. Log in with your GitHub credentials
3. In the dashboard https://railway.app/dashboard:
   
    a. Hit New and then select "empty project"
   
    b. Give the project a name, e.g. "QuoteMicroserviceApp" as I have done
   
    c. Within the project created, e.g. in my case https://railway.app/project/3cea3616-2b00-4d7c-9bf5-51263d4bdc9d, click on top right hand side button "+Create"
   
    d. Select GitHub repo and paste there the URL of the source code repo having a Dockerfile which you want to deploy as a service.
      - I have done this with the contents of the following three public repositories:
         - https://github.com/dipina/QuoteFrontEnd
         - https://github.com/dipina/APIGateway-railways
         - https://github.com/dipina/QuoteService-railways
      - IMPORTANT.For each microservice, within the "Setting tab" search for "domain" and click on option to add public domain within "Public Networking" in order to access your application over HTTP

5. As result you will have created 3 microservices with the Railway project which are accessible via HTTP. Those services may share ENVIRONMENT VARIABLES among them.
   
    a. For our microservices we have to inform the API Gateway microservice of the public domain where QuoteService-railways has been deployed. For that, we define some SHARED VARIABLES for all the microservices, with the project settings.
        * Go to the project page and select "Settings" on the top right hand side
        * Then, click on "Shared variables"
        * Define QUOTES_API_GATEWAY with value https://quoteservice-railways-production.up.railway.app/
   
    b. Click on "Architecture" at the top part and select "APIGateway-railways"
   
    c. Click on "Variables" within the service
   
    d. Click on "Shared variable" and ADD to this Service the ENVIRONMENT VARIABLE for the project named QUOTES_API
   
7. Notice that the URL of the API Gateway is hardcoded within file src/script.js of QuoteFrontEnd.
    a. Now is set up to const API_GATEWAY = "https://apigateway-railways-production.up.railway.app";
   
    b. You should update the value with the public DNS name for the APP Gateway

9. You should now be able to access the app consisting of 3 microservices fully deployed in the Cloud: https://quotefrontend-production.up.railway.app/


