# Docker : PostgreSQL with CStore extension

## What is CStore ?

See [https://github.com/citusdata/cstore_fdw](https://github.com/citusdata/cstore_fdw) for details, examples.

It's a columnar store for analytics with Postgres, developed by Citus Data, bringing some astonishing performance for some data schema.

## Why both in Docker ?

It's so useful !

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
	$ docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=postgres -v "$PWD/my-postgres.conf":/etc/postgresql/postgresql.conf mnementh64/docker-postgresql-cstore




