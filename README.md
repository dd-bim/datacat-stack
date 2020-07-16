# datacat application stack

This repository combines all needed components to execute datacat locally.
To run this application the container runtime Docker as well as the cli tool
docker-compose (packaged with Docker on MacOS and Windows) must be available.

Docker install documentation: https://docs.docker.com/desktop/

After installing Docker and starting the runtime you'll be able to start datacat by:

````bash
# Clone this repository into a writable location
$ git clone https://kis5.geoinformation.htw-dresden.de/gitlab/bentrm/datacat-stack.git datacat

# Move into the new directory
$ cd datacat

# Run the docker-compose stack
$ docker-compose up

# Updating the stack if new container images become available
$ docker-compose pull

# Deleting/resetting the stack
$ docker-compose down
$ docker volume prune
````

The first startup might take a while as the application will wait for the database
to completely initialize.

You can stop the application stack by Ctrl+C in the terminal.
To reset the database empty the `data` folder.

The application will be available after all component containers have been downloaded
and initialized on http://localhost:3000.

The default admin user account created during startup has the credentials `admin:s3cret`.
The is now email provider configured in this setup. Signup requests will be logged to the 
terminal.

