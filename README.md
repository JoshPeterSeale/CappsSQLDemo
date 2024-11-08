# CAPPS DEMO

This repository contains the code required to spin up a postgreSQL and nifi docker container. A mount point has been created for the nifi container such that csv files on the host system can be accessed by nifi, with the data inserted into a SQL container.

## Pre-requisites:

- Ensure docker is installed
- In the same directory as the docker-compose.yml file run the following line of code to spin up the two docker containers:
`sudo docker compose up -d`

## To access the nifi ui

- Go to https://localhost:8443/nifi
- username is admin
- password is admin_password
N.b. Username and password is configurable via the docker-compose at the moment

## Import the template

Since I have not included my docker volume as part of the gitlab repository, to start using the nifi flow I have created you must first import the demo_template.xml file found in the nifi directory. 
- Right click on the canvas
- Click Upload Template
- Select the demo_template.xml

Following this must then turn on all of the processors:
- Right click on each processor and press start

Must also start the controller services:
- Go in to ConvertRecord, click the arrow next to CSV Reader and press the Enable Icon. Repear for JSONRecord.
- Go in to ConvertJSONToSQL, click arrow next to DBCPConnectionPool, press configure and add the password capps_passto the Password property value slot. Click apply and start up the service using the enable icon

## To access the psql db

To enter the postgreSQL container in a psql terminal run:
`sudo docker exec -it capps-sql psql -d capps_db -U capps_user`
If prompted for a password, it is capps_pass. 
This is configurable via capps-setup.sh script which initialises the capps_db database and creates the demo table with columns a (int) and b (varchar(100))

## To test the flow

There are two simple test csv files in nifi/test_data. These can be copied in to nifi/mounts/files to be read by the nifi container. A user guide for how to pause and view the results of processors can be found here: https://nifi.apache.org/docs/nifi-docs/html/user-guide.html
