## featherweight_login
Login and obtain a token for use with the MySQL REST API Service (MRS)

### About the Featherweight Framework Project (FFP)
The purpose of the Featherweight Framework Project is to develop a methodology that exploits the capabilities of the MySQL Rest API Services (MRS). The strategy is to minimize middleware API services and move CRUD and transactional logic to the database using stored procedures and views. The goal is to create a highly performant backend whose access to data and services are controlled and centralized through Database Developers and Administrators.

### About Northern Pacific Technologies, LLC (NorPacTech)
NorPacTech is a small company that primarily utilizes AWS, the Spring Framework, MySQL for its development stack. The Featherweight Framework will be the next generation platform. As of this writing, the framework is in its infancy, but to learn more, please reach out to [Scott Klakken](scott@northernpacific.tech).

### Running this software
This software is to be used in a serverless backend though it can be run locally on a development laptop/desktop by entering the following command:

`npm run start`

By default, the API will listen on port 3000.

For use in the cloud, refer to the Serverless Framework project, and serverless.yml file. As built, the software is setup to run on AWS in the Oregon Region. To install into the AWS cloud, the following is entered on the command line:

`sls deploy --stage dev`

As shown, this will run the software into the 'dev' environment. A 'prod' configuration is also available in the project's serverless.yml file.

### Using this software
The starting point for the featherweight_login was the blog [Introducing the MySQL REST Service](https://blogs.oracle.com/mysql/post/introducing-the-mysql-rest-service) by Michael Zinner. The blog illustrates the method for "Configuring MRS and Creating a MRS Service" using Visual Studio Code (whose functionality is impressive). 

If you're using a Windows machine, ensure you run all scripts using Powershell, as the DOS command line won't work.

There is an example Progressive Web App (PWA) that accompanies MySQL Shell for VS Code. The auth/crypto portion in this software was reversed-engineered from the PWA to provide the capability to obtain a token.

MRS supports popular OAuth2 services, but to keep things simple, the MySQL 'MRS' authentication is used.

First, create an "Authentication App" that's tied to the service:

Add New Authentication App by right-clicking on the "/myService" menu item.
Select 'Add New Authentication App". Vendor is "MRS"
Next, create a User within the authentication app:

Right-Click on the "MRS (MRS)" authentication item that was created in the previous step.
Add User
Once the "/myService" and user is setup, a token can be obtain using the following curl command:

`curl --location 'http://localhost:3000/local/mrs-auth/login' --header 'Content-Type: application/json' --data '{ "username": "scott", "password": "password" }'`

Which retrieves the following:

`{ "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoiMTFlZjE1ZjIxMjEyYzU4NWI1ZmEwMGZmYWY0YmYwMjQiLCJleHAiOiIyMDI0LTA1LTI1IDE2OjQ4OjMyIiwic2VydmljZV9pZCI6Ilx1MDAxMe9cdTAwMTXwW9eqV7X6XHUwMDAw_69L8CQifQ.oDGFv88Av2Y1zGysY92EnjWxKmXvIh--JpWh-O_ND4o" }`

### Postman
This project contains a "postman" subdirectory that has an export of the featherweight_auth and myService APIs in action. Note that after clicking on the mrs_example folder, the "Authorization" and "Variables" tab are popluated with example entries. Update the values to miror your environment:

Select the "Authorization" tab and enter your username/password, url, etc...
Select the "Variables" tab and enter your url, service, and schema accordingly.

### Wrap-Up
Hopefully, this software will be useful. If you have any questions, please feel free to reach out...

[Scott Klakken](scott@northernpacific.tech)
