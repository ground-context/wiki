---
title: Hit the Ground Running
keywords: getting_started
sidebar: ground_sidebar
permalink: index.html
folder: overview
---

You can download the latest version of Ground from our [releases page](https://github.com/ground-context/ground/releases).
The most recent version of Ground is [**v0.1**](https://github.com/ground-context/ground/releases/tag/v0.1.0).

Once you have downloaded the latest version of Ground, you can start the Ground server by running `./bin/ground-postgres`.*
This starts a local Ground server running on port 9000.

For more about how we envision common use cases in Ground, please see the [Usage](usage.html) documentation.

\* **NOTE**: Ground currently only support Postgres as a storage backend. Future releases will add support for Cassandra and Neo4j amongst other.

## Configuring Ground

**Port**: To change the port that Ground is running on, pass the argument `-Dhttp.port={your-port}` when starting the Ground server.

**Postgres**: By default, Ground expects Postgres to be at `localhost:5432`. If you are running a different Postgres server, you can set `db.default.url` in `conf/application.conf` before starting the Ground server.

## Building Ground from Source

If you'd like to build Ground from source, we highly recommend that you build from the tagged version instead of the latest version of the master branch. 
Given that the project is in a very early stage, it is likely that the master branch will be very volatile.

If you do not have SBT locally, a version of SBT is in the git repository.
To build Ground using this version of SBT, run: `chmod +x sbt-dist/bin/sbt; sbt-dist/bin/sbt dist`.
To learn more about how to use SBT, please visit the [SBT webiste](http://www.scala-sbt.org/).
