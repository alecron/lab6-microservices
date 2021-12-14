# Report
## The two services are running and registered
The registration service must be run before the other services. You can run all of the services by using the following commands:
```
./gradlew :registration:bootRun
./gradlew :accounts:bootRun
./gradlew :web:bootRun
```

When both accounts and web services start running they retgister into the Eureka service automatically.

###Logs
Accounts
![Accounts_log](images/accounts2222.png)

Web
![WS_log](images/webservice.png)


## The service registration service has two services registered
Once the services are running and registered you can access the Eureka dashborad in order to check their status:
![eurekaDashboard_2services](images/eurekaDB2servicios.png)

## A second account service is running in the port 4444 and it is registered
In the `application.yml` file that can be found inside the `accounts/src/main/resources` folder stablishes the ports for the service. Changing the `port:2222` to `port:4444` allows a new accounts service to run on that port.
![Accounts2_log](images/accounts4444.png)

If we run a new accounts service the dashboard shows 2 `ACCOUNTS-SERVICE` running and registered.

![eurekaDashboard_3services](images/eurekaDB3servicios.png)

## What happens when you kill the service with port 2222? Can the web service provide information about the accounts? Why?
Killing the service in 2222 makes it dissappears from the registration service and so it does from the Eureka Dashboard.
![eurekaDashboard_4444](images/eurekaDB4444.png)


During a short period of time Eureka redirects to the dead service. If you ask for any information during that time the web service returns an Internal Server Error (500).
When you ask for an account after Eureka has detected the dead service it returns the user information without any problem.
![error500](images/error500.png)
![account](images/cuentaObtenida.png)

It works because Eureka acts as a mediator between the web service and the accounts service. The web server asks for the `ACCOUNTS-SERVICE` and Eureka returns the route to it.

