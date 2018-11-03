# Docker : PostgreSQL with CStore extension

![Docker Build Status](https://img.shields.io/docker/build/mnementh64/docker-postgresql-cstore.svg)
![Docker build](https://img.shields.io/docker/automated/mnementh64/docker-postgresql-cstore.svg)
[![License](https://img.shields.io/github/license/mnementh64/docker-postgresql-cstore.svg)](LICENSE)

## What is CStore ?

See [https://github.com/citusdata/cstore_fdw](https://github.com/citusdata/cstore_fdw) for details, examples.

It's a columnar store for analytics with Postgres, developed by Citus Data, bringing some astonishing performance for some data schema.

## How to run it ?

As the Docker entrypoint is the same as in the official PostgreSQL docker image, for custom environment, see details on the [Dockerhub page](https://hub.docker.com/_/postgres/).

For a simple container exposing its 5432 port without any mounted volume, with `postgres` as password for `postgres` user, you can run 

	$ docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=postgres mnementh64/docker-postgresql-cstore

To mount data in host storage, launch

	$ docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=postgres -v host_path_to_data:/var/lib/postgresql/data mnementh64/docker-postgresql-cstore

To use a custom PostgreSQL configuration :

	# copy template from the container
	$ docker run -i --rm mnementh64/docker-postgresql-cstore cat /usr/share/postgresql/postgresql.conf.sample > my-postgres.conf

	# customize it ...

	# run postgres with custom config
	$ docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=postgres -v "$PWD/my-postgres.conf":/etc/postgresql/postgresql.conf mnementh64/docker-postgresql-cstore -c 'config_file=/etc/postgresql/postgresql.conf'
	
In a docker-compose :

	version: "2"
	services:
	  postgres:
	    image: mnementh64/docker-postgresql-cstore:10.3
	    ports:
	      - 5432:5432
	    volumes:
	      - /tmp:/tmp
	      # to use a custom config
	      #- ./my-postgres.conf:/etc/postgresql/postgresql.conf
	      # to persist data to host
	      #- /path_on_host/data:/var/lib/postgresql/data
	    # to use a custom config
	    #command: postgres -c config_file=/etc/postgresql/postgresql.conf
	    environment:
	      # user : postgres
	      POSTGRES_PASSWORD: "your_password"





