# datacat application stack

This repository combines all components to execute the datacat API and editor client application.
To make use of this project, Docker must be installed. Also, the `docker compose` executable must be available.

Docker install documentation: https://docs.docker.com/desktop/

The stack contains of:
- neo4j: the graph database
- datacat api: the business logic with a GraphQL API
- datacat editor: the web frontend to view and edit concepts in dictionaries, import or export concepts or create ids files
- datacat restapi: this rest api has the same endpoints like the bSDD API (only endpoints needed for classification)

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

### Run stack

To pull the images and start the application stack run in the project directory:

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
# Update to the image version you'd like to use
$ nano .env

# Stopp the running containers
$ docker compose down

# Pull and start the new application stack
$ docker compose up -d
````

# Debugging

For debugging purposes, it might be useful to access the database directly.
This is possible from the host system by executing the cypher-shell of the database
container directly:

````bash
$ docker compose exec db cypher-shell
````
