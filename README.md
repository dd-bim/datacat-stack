# datacat application stack

This repository combines all components to execute the datacat API and editor client application.
To make use of this project, Docker must be installed. Also, the `docker compose` executable must be available.

Docker install documentation: https://docs.docker.com/desktop/

The datacat editor application is build as part of this configuration into a static nginx container that
functions as the applications' frontend proxy as well. Check the build directory `./services` how this is handled.
By default, the administration interface of the bundled Neo4j database is not exposed / proxied. 

## Installation

To run the application stack, clone this repository into a writable location.

````bash
$ git clone https://github.com/dd-bim/datacat-stack.git
````

### `.env`
Move into the new directory, create a copy of the given example configuration file
`env.example.txt` as `.env` and edit the settings according to your needs.

To make sure your installation is reproducible in production, you should define an explicit version
as available at [Docker Hub](https://hub.docker.com/repository/docker/schi11er/datacat).

````bash
$ cd datacat-stack
$ cp env.example.txt .env
$ nano .env
````

### `docker-compose.override.yml`
Optionally, you might override the given settings in the `docker-compose.yml` file by copying `docker-compose.override.example.yml`
as `docker-compose.override.yml`. 
The example given includes the development SMTP server [MailSlurper](https://github.com/mailslurper/mailslurper). In production,
you must define a relaying SMTP server, as the users will need to verify their email address on signup.

**Ideally, `docker-compose.yml` should stay untouched to track upstream development. All environmental settings
should be overriden by editing `docker-compose.override.yml`.**

### Pull current images

To pull the current container images according to your configuration run:

````bash
$ docker compose pull
````

### Build client / proxy container

To build the client / proxy image of the application stack run:

````
$ docker compose build
````

### Run stack

To start the application stack run in the project directory:

````
$ docker compose up -d
````

Access the logs by running `docker compose logs`.

### Stop stack

To stop the application stack, run:

````bash
$ docker compose down
````

The current state is persisted in the linked docker volumes. Check the datacat projects' readme
on how to back up and restore the database.

### Update

````bash
# Pull updates of the datacat-stack project
$ git pull origin master

# Update to the datacat / editor image version you'd like to use
$ nano .env

# Pull new versions of the container images
$ docker compose pull

# Build and (re-)start the application stack 
$ docker compose up --build -d
````

# Debugging

For debugging purposes, it might be useful to access the database directly.
This is possible from the host system by executing the cypher-shell of the database
container directly:

````bash
$ docker compose exec db cypher-shell
````
