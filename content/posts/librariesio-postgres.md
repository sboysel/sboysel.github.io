---
title: "Working with the Libraries.io database"
author: Sam Boysel
date: 2022-07-12T06:42:37-07:00
draft: true
---

Load an offline copy of the [Libraries.io](https://libraries.io/) database into
a Dockerized Postgres instance.

### Motivation

For a recent project, I had a need to gather data on the relationships between
software packages over time.  In most major packaging ecosystems, published
versions of software projects explicity state the set of external project they
depend on in some form of project manifest.  An excellent source for this type
of data is Libraries.io, an effort by Tidelift to map relationships between
publicly released software packages.  From the
[About](https://libraries.io/about) page:

> Libraries.io indexes data from 5,557,755 packages from 32 package managers. We
> monitor package releases, analyse each project's code, community, distribution
> and documentation, and we map the relationships between packages when they're
> declared as a dependency. The 'dependency tree' that emerges is the core of the
> services that we provide.

As the set of projects indexed by Libraries.io is
incredibly vast, I decided on sampling a subset of key Node.js packages and
along with indirect dependent (downstream) and dependency (upstream) neighbors.

Complex processing data too large to fit into memory is often easier in a
database management system (DBMS).  A common extract, transform, load (ETL)
pattern is to download arhived data from the internet, extract and clean a
subset of it, and load it into a DBMS for easier analysis.

- Reproducible
- Portable

### Dependencies

- [docker](https://www.docker.com/) and [docker-compose](https://docs.docker.com/compose/)
- (optional) [GNU Make](https://www.gnu.org/software/make/)

### Usage

Clone the repository

```bash
git clone git@github.com:sboysel/librariesio-postgres.git
cd librariesio-postgres
```

Edit environment variable `LIBIO_HOME` in `.env` to point to the directory where
the database will be stored.

```
LIBIO_URL=https://zenodo.org/record/3626071/files/libraries-1.6.0-2020-01-12.tar.gz
LIBIO_TARGZ=libraries-1.6.0-2020-01-12.tar.gz
LIBIO_HOME=/path/to/librariesio
```

The archive is downloaded to `LIBIO_HOME` and component tables are extracted to
the directory as CSV files.  Intermediate processing is also done in this directory.

In repository root, run GNU make to build the application container, bring up
services, and run the application (download, extract, copy CSV to post
)
```bash
make
```

Use visit pgweb UI in browser at [0.0.0.0:8081](0.0.0.0:81) or use `psql` to
connect to `postgres` instance
```bash
PGPASSWORD=postgres psql -U postgres -d librariesio -h 0.0.0.0
```

### Details

### Resources

- https://zenodo.org/record/3626071#.YprimnXMJQJ
- https://geshan.com.np/blog/2021/12/docker-postgres/
- https://herewecode.io/blog/create-a-postgresql-database-using-docker-compose/
- https://graspingtech.com/docker-compose-postgresql/
- https://thedatasoup.com/data-ingestion-running-a-pipeline-with-python-postgres-and-pgadmin-using-docker/
- https://hub.docker.com/r/sosedoff/pgweb/
