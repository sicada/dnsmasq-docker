# dnsmasq-docker
Code for building dnsmasq DNS and DHCP server as a docker service. This
dnsmasq is wrapped in the simple webproc program by jpillora 
(https://github.com/jpillora/webproc), which provides a simple web interface
for managing the service. 

A docker-compose.yml file is also included to show one way to run the docker
container from docker-compose. 

Once the container is running, the web interface can be accessed from a
web browser at http://localhost:8080/
