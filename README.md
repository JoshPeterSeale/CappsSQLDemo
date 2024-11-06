# CAPPS DEMO

This repository contains the code required to spin up a postgreSQL and nifi docker container. A mount point has been created for the nifi container such that csv files on the host system can be accessed by nifi, with the data inserted into a SQL container.

## Pre-requisites:

- Ensure docker is installed
- Build the postgresql database image using docker:
`cd db`
`sudo docker build . -t capps-db:test`
- In the same directory as the docker-compose.yml file run the following line of code to spin up the two docker containers:
`sudo docker compose up -d`

## To access the nifi ui

- Go to https://localhost:8443/nifi
- username is admin
- password is admin_password
N.b. Username and password is configurable via the docker-compose at the moment

## To access the psql db

To enter the postgreSQL container in a psql terminal run:
`sudo docker exec -it capps-sql psql -d capps_db -U capps_user`
If prompted for a password, it is capps_pass. 
This is configurable via capps-setup.sh script which initialises the capps_db database and creates the demo table with columns a (int) and b (varchar(100))

## To test the flow

There are two simple test csv files in nifi/test_data. These can be copied in to nifi/mounts/files to be read by the nifi container. A user guide for how to pause and view the results of processors can be found here: https://nifi.apache.org/docs/nifi-docs/html/user-guide.html

