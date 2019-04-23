# JmeterDocker
JMBASE -   Base image container having JMETER, JDK8 and few utilities like wget, unzip, telnet etc
JMMASTER - Master docker file should be inherited from the JMBASE image and should expose port 60000.
JMSERVER - Server docker file should be inherited from the JMBASE image and should expose port 1099 and 50000. jmeter-server should be running.

Ensure that docker is installed in your machine
The above docker files are available in my repository myanees

Run the below command to create a container for JMeter slave.
# docker run -dit --name slave01 myanees/jmserver /bin/bash

Run the below command to create a container for JMeter master.
# docker run -dit --name master myanees/jmmaster /bin/bash

Check the running container
# docker ps -a

Run the below command to get the list of ip addresses for these containers
# docker inspect --format '{{ .Name }} => {{ .NetworkSettings.IPAddress }}' $(sudo docker ps -a -q)

In case – you need to copy any files from the host to the docker container – You can issue below command. For ex: I copy the test into my JMeter master container. This command will copy my local jmeter test (docker-test.jmx) into the master container in this path: /jmeter/apache-jmeter-3.3/bin/drybar.jmx

# sudo docker exec -i master sh -c 'cat > /jmeter/apache-jmeter-3.3/bin/drybar.jmx' < drybar.jmx
