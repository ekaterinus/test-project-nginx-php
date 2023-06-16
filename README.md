## Nginx, Php8.2, Docker Swarm Project

This project consists of 2 components: Nginx and Php 8.2. It is a simple project, which displays phpinfo page.

I made it all on local VM and created a ssh tunnel to connect to the server and check results:

`ssh -o ExitOnForwardFailure=yes -fN -L 8080:localhost:80 -p 2222 root@127.0.0.1`

#### To start the project:
1) `cd /to/directory/with/docker-compose.yml/`
2) `docker swarm init`
3) `docker stack deploy -c docker-compose.yml <test_name>`

#### To check logs:
1) If you want to see nginx logs: `service logs <test_name>_nginx`
2) If you want to see php logs: `service logs <test_name>_php`

#### Additionally 
I want to briefly describe the reason for choosing docker swarm and the problems encountered in the implementation of the solution.

The reason is very simple, because in my opinion this way of deploying the application is clearer (as for me) and easier. There also were some problems, when I was implementing the solution, such as properly nginx configuration to display the page correctly and setting up the docker-compose.yml file so that nginx and php can see each other.

___

#### Theoretical Part
For Theoretical Part I decided to describe process of deploying to AWS from GitLab CI/CD. The architectural diagram is located in `"Gitlab_CICD_and_AWS_Services.pdf"`

I will try to briefly describe my understanding of the diagram:

The Frontend and Backend parts are communicating with each other. Backend is also connected to the database.
The Frontend is deployed to Amazon S3 for hosting static files, and it can be distributed through Amazon CDN and caching.
The Backend is represented by AWS Lambda for executing the business logic. The Backend can also access data from Amazon DynamoDB.
The GitLab CI/CD pipeline includes the steps of building frontend and backend, deploying them to the appropriate AWS services, executing tests, monitoring, and performing cleanup as necessary.
