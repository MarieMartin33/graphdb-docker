This keeps the infrastructure that builds docker images for [GraphDB](http://graphdb.ontotext.com/)

Check [Docker Hub Images](https://hub.docker.com/r/ontotext/graphdb/) for information on how to use the images.

# Quick build

```bash
# git clone https://github.com/Ontotext-AD/graphdb-docker.git
git clone https://github.com/MarieMartin33/graphdb-docker.git
cd graphdb-docker
# ckeck makefile
vi Makefile
# check docker file
vi Dockerfile
make build-image VERSION=10.6.3
# cd preload to preload, other option is cd loadrdf
cd preload
# check .env
vi .env
# check docker-compose.yla
vi docker-compose.yml
# check graphdb-repo.ttl
vi graphdb-repo.ttl
# build graph-data
docker-compose build
docker-compose up -d
# build and run docker image
cd ..
docker-compose up -d --build
```

# Building a docker image

You will need docker and make installed on your machine.

1. Checkout this repository
1. Run
```bash
make build-image VERSION=<the-version-that-you-want>
```

for example the most recent version as of this writing is 10.6.3 so run
```bash
make build-image VERSION=10.6.3
```

this will build an image that you can use called ontotext/graphdb:10.6.3
You can run the image now with

```bash
docker run -d -p 7200:7200 ontotext/graphdb:10.6.3
```

Consult the docker hub documentation for more information.

### Preload a repository

Go to the `preload` folder to run the bulk load data when GraphDB is stopped.

```bash
cd preload
```

By default it will:

* Create or override a repository defined in the `graphdb-repo-config.ttl` file (can be changed manually in the file, default is `demo`)
* Upload a test ntriple file from the `preload/import` subfolder.

> See the [GraphDB preload documentation](https://graphdb.ontotext.com/documentation/10.2/loading-data-using-importrdf.html) for more details.

When running the preload docker-compose various parameters can be provided in the `preload/.env` file:

```bash
GRAPHDB_VERSION=10.6.3
GRAPHDB_HEAP_SIZE=3g
GRAPHDB_HOME=../graphdb-data
REPOSITORY_CONFIG_FILE=./graphdb-repo.ttl
```

Build and run:

```bash
docker-compose build
docker-compose up -d
```

> GraphDB data will go to `/data/graphdb`

Go back to the root of the git repository to start GraphDB:

```bash
cd ..
```

### Start GraphDB

To start GraphDB run the following **from the root of the git repository**:

```bash
docker-compose up -d --build
```

> It will use the repo created by the preload in `graphdb-data/`

> Feel free to add a `.env` file similar to the preload repository to define variables.


# Issues

You can report issues in the GitHub issue tracker or at graphdb-support at ontotext.com


# Contributing

You are invited to contribute new features, fixes, or updates, large or small;
we are always thrilled to receive pull requests, and do our best to process
them as fast as we can.

Before you start to code, we recommend discussing your plans through a GitHub
issue, especially for more ambitious contributions. This gives other
contributors a chance to point you in the right direction, give you feedback on
your design, and help you find out if someone else is working on the same
thing.
