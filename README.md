# eCISE ontology / SATAIS database mapping

Version 1.0.0

**Table of Contents**

- [1. General purpose](#general-purpose)
- [2. Repository structure](#repository-structure)
- [3. Deploy SPARQL endpoint using Ontop Docker](#deploy-sparql-endpoint-using-ontop-docker)

## General purpose

eCISE ontology / SATAIS database mapping aims at retrieving data stored in the SATAIS database by using the eCISE ontology and the SPARQL Ontop endpoint.

## Repository structure

~~~
.
├── data
│   └── pgsql (ignored for git)
│       ├── base
│       ├── global
│       ├── pg_commit_ts
│       ├── pg_dynschem
│       ├── pg_logical
│       ├── pg_multixact
│       ├── pg_notify
│       ├── pg_replslot
│       ├── pg_serial
│       ├── pg_snapshots
│       ├── pg_stat
│       ├── pg_stat_tmp
│       ├── pg_subtrans
│       ├── pg_tblspc
│       ├── pg_twophase
│       ├── pg_wal
│       ├── pg_xact
│       ├── pg_hba.conf
│       ├── pg_indent.conf
│       ├── PG_VERSION
│       ├── postgresql.auto.conf
│       ├── postgresql.conf
│       ├── postmaster.opts
│       └── postmaster.pid
├── jdbc
│   └── postgresql-42.3.3.jar
├── obda
│   ├── catalog-v001.xml
│   ├── ecise_db.obda
│   ├── ecise-ontology-1.4.1.owl
│   ├── ecise_db.properties
│   ├── ecise_db.q
│   ├── ecise_db.r2rml
│   ├── ecise_db.toml
│   └── wait-for-it.sh
├── .env
├── docker-compose.yaml
├── LICENSE
└── README.md
~~~

- `data`: Postgresql SATAIS database
- `ecise_db.obda`: Mapping file (Ontop syntax)
- `ecise_db.r2rml`: Mapping file (R2RML syntax) => empty for now
- `ecise-ontology-1.4.1.owl`: Ontology file
- `ecise_db.properties`: Properties file
- `ecise_db.q`: Queries file for Protege


## Deploy SPARQL endpoint using Ontop Docker

### Requirements
* [Docker](https://docs.docker.com/get-docker/), version 17.09.0 or higher
* [Docker Compose](https://docs.docker.com/compose/install/), version 1.17.0 or higher

### Steps

1) to start the prototype, downloading / building the required images and containers if needed
  ```
  docker-compose up
  ```
  (note: may add option `-d` to run in background, in which case logs are not be displayed to standard output but are still accessible via `docker-compose logs`)

**Services** When running, the prototype exposes the following services:

* a PostgreSQL server with the sample data, with connection information defined in the [.env](`.env`) file. 

* a Web portal of the SPARQL endpoint backed by ontop at URL <http://localhost:8080/>
  
* a SPARQL endpoint backed by ontop at URL <http://localhost:8080/sparql>

* a PgAdmin web portal to visualize the SATAIS database at <http://localhost:5050/>

2) to stop the prototype, if running
  ```
  docker-compose down
  ```

3) to stop the prototype, if running, and also clean any image / container / data associating to it (useful for cleaning up)
  ```
  docker-compose down --volumes --remove-orphans
  ```
  (note: the above command does not remove Docker images that may result being unused after stopping and removing this prototype containers; to remove such images, add option `--rmi all`)

4) to check the status of the containers forming the prototype
  ```
  docker-compose ps
  ```

5) to check the logs of specific container(s) or of all containers (if no container name is supplied)
  ```
  docker-compose logs <container name 1> ... <contaner name N>
  ```
