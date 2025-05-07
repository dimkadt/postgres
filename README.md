# PostgreSQL Database Replication

Basic ready-to-use PostgreSQL cluster, which implements asynchronous Primary-Secondary data replication within a pair of preconfigured database containers and load balancing.

## Package Implementation Specifics

The presented PostgreSQL Replication solution is based on Virtuozzo Application Platform(VAP) certified stack templates which built:
 - for **[PostgreSQL](https://www.postgresql.org/)** database
 - for **[Pgpool-II](https://www.pgpool.net/mediawiki/index.php/Main_Page)** load balancer
 
 By default, package operates two database containers (Primary and Secondary, one per role) and makes data from Primary DB server to be asynchronously replicated to a standby one.
 In front of the cluster a scalable load balancer layer of Pgpool-II node can be added which provides load-balancing, monitoring and management of database cluster.

<p align="left">
<img src="images/pgpool-postgres-single-region-big-tip-black-font.svg" width="450">
</p>

Within the package, each database container receives the [vertical scaling](https://www.virtuozzo.com/application-platform-docs/automatic-vertical-scaling/) up to **32 dynamic cloudlets** (or 4 GiB of RAM and 12.8 GHz of CPU) that are provided dynamically based on the incoming load. And for the load balancer node the **6 dynamic cloudlets** provided by default. Subsequently, you can change the resource allocation limit by following the above-linked guide.

## How to Install PostgreSQL Database Replication Package

In order to get PostgreSQL Database Replication solution instantly deployed, click the **Deploy to Cloud** button below and specify your email address within the opened widget. Then choose one of the [Virtuozzo Public Cloud](https://www.virtuozzo.com/application-platform-partners/) providers (in case you don’t have an account at the appropriate platform, it will be created automatically) and press **Install**.

[![Deploy](images/deploy-to-cloud.png)](https://jelastic.com/install-application/?manifest=https://raw.githubusercontent.com/jelastic-jps/postgres/v2.1.0/manifest.yaml)

To install the package manually, log in to the Virtuozzo Application Platform dashboard with your credentials and [import](https://www.virtuozzo.com/application-platform-docs/environment-import/) link to the [**_manifest.yaml_**](https://github.com/jelastic-jps/postgres/blob/master/manifest.yaml) file (alternatively, you can locate this package via [VAP Marketplace](https://www.virtuozzo.com/application-platform-docs/marketplace/), *Clusters* section)

<p align="left">
<img src="images/postgresql-replication-installation.png" width="550">
</p>


Within the opened installation window, choose the PostgreSQL database version among available ones, type *Environment* name and optional *Display Name* ([environment alias](https://www.virtuozzo.com/application-platform-docs/environment-aliases/). Also, select the preferable [*Region*](https://www.virtuozzo.com/application-platform-docs/environment-regions/) (if several ones are available) and click **Install**.
If required you may disable Pgpool-II load balancer layer with respective toggle. 

Wait a few minutes for VAP to prepare your environment and set up the required replication configurations. When finished, you’ll be shown the appropriate notification with data for PostgreSQL administration interface access. 

<p align="left">
<img src="images/postgresql-replication-success-message.png" width="400">
</p>


This information will be also duplicated to you via email.

### Cluster Entry Point

In case of no Pgpool-II nodes were added to cluster topology, use Primary node to access the cluster. And if the load balancing layer was deployed in front of the db cluster you may use any of Pgpool-II nodes as the entry point.

### Cluster Management

In VAP the PostgreSQL cluster components can be managed either via [CLI](https://www.virtuozzo.com/application-platform-docs/ssh-access/) or UI.

#### Database Management

Database nodes have a built-in management administration panel phpPgAdmin. Use the only one on Primary node.

<p align="left">
<img src="images/phppgadmin.png" width="600">
</p> 

If required, the separate node can be installed with more advanced PostgreSQL database management software [pgAdmin4](https://www.pgadmin.org/) via importing [manifest](https://github.com/jelastic-jps/pgadmin/blob/master/manifest.yaml) from VAP collection.

<p align="left">
<img src="images/pgadmin.png" width="600">
</p>

#### Pgpool-II Management

Pgpool-II nodes can be also managed via user-friendly built-in Administration Panel [pgpoolAdmin](https://www.pgpool.net/docs/pgpoolAdmin/index_en.html).

<p align="left">
<img src="images/pgpool-admin.png" width="600">
</p>

Pgpool-II admin panel provides an ability to tune: 
 - load balancing and even at database level. It means that you can specify how the requests to every database should be processed and balanced
 - connection pools
 - logging
 - replication
 - debugging
 - failover and failback
 - etc.


To find more details on PostgreSQL Replication package installation and use, refer to the [article](https://www.virtuozzo.com/company/blog/postgresql-auto-clustering-master-slave-replication/).
