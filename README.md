# Atlassian Stash

On-premises source code management for Git that's secure, fast, and enterprise grade. Create and manage repositories, set up fine-grained permissions, and collaborate on code – all with the flexibility of your servers.

This is inspired by [Hbokh/docker-jira-postgresql](https://github.com/hbokh/docker-jira-postgresql)
but the installation and run process is made in a more generic way, to serve as base
for the installation of other Atlassian Products.

## Instalation

Is best practice to separate the data from the container. This instalation process
will assume this.

### 1. Create a data-only container for stash

Create a data-only container from Busybox (very small footprint) and name it "stash\_datastore":

    docker run -v /opt/crowd-home --name=stash\_datastore -d busybox echo "stash data"

**NOTE**: data-only containers don't have to run / be active to be used.

### 2. Create a PostgreSQL-container

See: [POSTGRESQL](POSTGRESQL.md)

### 3. Start the Software container

    docker run -d --name stash -p 7990:7990 -p 7999:7999 --link postgresql:db atende/stash \
    --volumes-from stash\_datastore

The port 7999 is used to SSH git access and 7990 for web access

## Running Behind a Proxy

In production environments is a best practice run the container on port 80 and
use a appropriated name like http://software.company.com

In this cases you could also need to run the software behind a proxy, so you can
run other applications in the same host.

This is a common feature of the atlassian images generetad by Atende Tecnology.

See the [Instructions](RUNNING_PROXY.md)
