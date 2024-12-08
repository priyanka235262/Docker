# Docker

Docker Commands

Docker commands are used to interact with Docker images, containers, and other components. Here's a breakdown of some common commands:

Image Management

docker images: List all locally available images.
docker pull <image_name>: Download an image from a registry (e.g., Docker Hub).
docker build -t <image_name> .: Build an image from a Dockerfile in the current directory.
docker rmi <image_name>: Remove an image.
docker image prune: Remove all unused images.
Container Management

docker run <image_name>: Create and run a container from an image.
docker ps: List running containers.
docker ps -a: List all containers (running and stopped).
docker start <container_id>: Start a stopped container.
docker stop <container_id>: Stop a running container.
docker restart <container_id>: Restart a running container.   
docker rm <container_id>: Remove a stopped container.
docker exec -it <container_id> <command>: Execute a command inside a running container.   
docker attach <container_id>: Attach to the standard output/error of a running container.
Other Useful Commands

docker info: Display system-wide information about Docker.
docker version: Show the Docker client and server versions.
docker login: Log in to a Docker registry (e.g., Docker Hub).
docker logout: Log out of a Docker registry.
docker system prune: Remove unused containers, images, networks, and volumes.
Example

To pull the official Nginx image from Docker Hub and run it as a container:

Bash

docker pull nginx
docker run -d -p 80:80 nginx
This command pulls the Nginx image, creates a detached container (runs in the background), and maps port 80 of the host machine to port 80 of the container.

For more detailed information and a comprehensive list of commands, refer to the official Docker documentation: https://docs.docker.com/engine/reference/commandline/docker/   

Docker Errors:
Docker Daemon Not Running:
Error: Cannot connect to the Docker Daemon. Is the docker daemonrunning on this host?
Cause: Docker daemon is not running.
Resolution:
 a.Start the Docker service:
 sudo systemctl start docker
 b.Verify the status
 sudo systemctl status docker

 2.Docker Permission Denied:
 Error: permission denied while trying to connect to the docker daemon socket ag
 Cause: User not added to the docker group.
 Resolution:
 Add the user to the Docker groupo:
 sudo usermod -aG docker $USER
 Logout and Log back in to apply changes.

 3.Port is already in Use:
 Error: Bind for 0.0.0.0:80 failed:port is already allocated.
 Cause:Port conflict with anothr process.
 Resoltuiob:
 Identify the process suing port:
 sudo netstat -tuln | grep 80
 Stop the conflicting service or use a diff port in the docker run command.
 docker run -p 8080:80...

 ImagePullError:
 error:error response from daemon,pull access denied.
 Cause:Image not found or requires authentication.
 Resolution: Verify the image name and tag
     Login to Docker Hub
docker login

Cannot Remove Container:
Error: Error response from daemon:container is in use by a running process.
Cause:Container is still running
Reso:
stop and remove the container.
docker stop <container_id>
docker rm < container-id>

Volume Not Mounting:
error: Eorror mounting Volume: Invalid path mount
Incorrect mount path
Reso:E
Ensure the source directory exists on the host.
Use absolute path fpr volume mounts.
 docker run v /host/path/container/path..

 7.Docker Build context too large
 Error:File size limit exceeded.
 Cause: Large files or directorues included in the buiuld context
 Reso:
 Use a dockerignore file to exclude unnecessary files
 .dockerignore
 mode_module/
 .git/

 Network Not Found:
 network <network-name> not found
 resol:
 create the n/w
 docker network create < netwoek-name>
 connect the container to the correct n/w

 Container exited immediately;
 error: exited (0) or Exited(1)
 Cause:Container provcess ends due to incorrect commands or script issues.
 reso:
 chcek container logs
 docker logs < container-id>
 Run the container interactively to debug:
 docker run -it <image-name> /bin/bash

 Disk space full
 Error: no space left on device
 Cause:
Docker is using too much disk space
reso:
Clesn up unused resources:
docker system prune -a 

Container name already in use:
error: conflict the container name already in use
cause:duplicate container name
Reso:
remove the conflicting container or use a unique name.

High CPU/Memory Usage
Cause: Resources-intensive conatiners.
reso:
limit resources in docker run
docker run --memory=512m --cpus=1...

Cannot push to provate registry
error:error response form daemon:denied:requested access
Cause:Authentication  Issue
Login to the regsitry
docker login <registry_url>

Container Restart Loop:
Error:exited(137)
Cause:Resources limits or errors in the entry point script
Reso:
check the logs to identify the issue
docker logs <container_id>


Network timeout
Error:Failed to connect to network:timeout
Cusse: Slow or interupted n/w connection
Reso:
Retry the operation or check the n/w stabiltiy
Increase time out with the timeout flag

Cnnot delete volume
error:Volume is in use
Cause:A container is still in use the volume
reso:
Remove the associated container before deleting the volume
docker rm -v <container_id>

Docker compose fails to start the srevices
error: service <service_name> failed to start
Incorrect docker-config.yaml syntax or missing dependencies.
validate the yaml file
docker-compose config
check the dependency order in depends_on

Logs not vaalaible:
Error:log files are missing or inaccessible
Caue:Logging driver misconfiguration
Reso:
check the logfging driver
docker info | grep logging


