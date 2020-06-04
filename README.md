# Notes

## General
- Container - system isolation method provided in Linux that’s more lightweight than a VM

- Docker - tool designed to make it easier to create, deploy, and run applications by using containers
				 - PaaS product that use OS-level virtualization to deliver software in packages called containers

- Docker image - a container is launched by running an image
				       - an image is an executable package that includes everything needed to run an application:
				       - the code, a runtime, libraries, environment variables, and configuration files

- Docker container - a runtime instance of an image - what the image becomes in memory when executed
				           - that is, an image with state, or a user process



Networking
==========
 - Linux network namespaces (netns) provides complete isolation 
 - each container runs in a separate namespace and can't communicate with another container by default
 - physical network interfaces are only accessible to apps running in the default namespace
 - IP addresses are automatically assigned to containers
 - VEth				- virtual cable for connecting two namespaces/containers
				- one end of the VEth gets renamed to eth0 inside the container, the other end connects to the bridge

 - Networking drivers (modes)

   - Bridge (dflt)		- connects multiple VEths together and to the host physical interface
				- default name is 'Docker0' and it runs in the default namespace
				- containers connected to the same bridge can communicate to each other but not to containers connected to a different bridge
				- containers can be connected to multiple bridges
				- NAT to communicate with the outside world
				- the default bridge network is NOT recommended for production; use a user-defined bridge instead

   - Host			- removes network isolation between the container and the Docker host
				- container uses the host’s networking directly
				- no NAT or namespace separation, all interfaces on the host can be used directly by the container
				- can be useful for standalone containers to optimize performance

   - Overlay			- creates an overlay network over physical network for container-to-container communication
				- each container gets 2 virtual interfaces and 2 bridges are creates
				- one bridge for physical network communication; another bridge for VxLAN communication (docker_gwbridge)

