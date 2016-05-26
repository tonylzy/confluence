![Atlassian Confluence Server](https://www.atlassian.com/dam/wac/legacy/confluence_logo_landing.png)
 
Confluence Server is where you create, organise and discuss work with your team. Capture the knowledge that's too often lost in email inboxes and shared network drives in Confluence – where it's easy to find, use, and update. Give every team, project, or department its own space to create the things they need, whether it's meeting notes, product requirements, file lists, or project plans, you can get more done in Confluence.
 
Learn more about Confluence Server: <https://www.atlassian.com/software/confluence>
 
# Overview
 
This Docker container makes it easy to get an instance of Confluence up and running.
 
# Quick Start
 
For the `CONFLUENCE_HOME` directory that is used to store Confluence data
(amongst other things) we recommend mounting a host directory as a [data volume](https://docs.docker.com/userguide/dockervolumes/#mount-a-host-directory-as-a-data-volume):
 
Set permissions for the data directory so that the runuser can write to it:
 
    $> docker run -u root -v /data/bitbucket:/var/atlassian/application-data/bitbucket atlassian/bitbucket-server chown -R daemon  /var/atlassian/application-data/bitbucket
 
Start Atlassian Confluence Server:
 
    $> docker run -v /data/bitbucket:/var/atlassian/application-data/bitbucket --name="bitbucket" -d -p 7990:7990 -p 7999:7999 atlassian/bitbucket-server
 
**Success**. Confluence is now available on [http://localhost:8090](http://localhost:8090)*
 
Please ensure your container has the necessary resources allocated to it.
We recommend 2GiB of memory allocated to accommodate both the application server
and the git processes.
See [Supported Platforms](https://confluence.atlassian.com/display/DOC/Supported+platforms) for further information.
     
 
_* Note: If you are using `docker-machine` on Mac OS X, please use `open http://$(docker-machine ip default):8090` instead._
 
# Upgrade
 
To upgrade to a more recent version of Confluence Server you can simply stop the `Confluence`
container and start a new one based on a more recent image:
 
    $> docker stop confluence
    $> docker rm confluence
    $> docker run ... (see above)
 
As your data is stored in the data volume directory on the host, it will still
be available after the upgrade.
 
_Note: Please make sure that you **don't** accidentally remove the `confluence`
container and its volumes using the `-v` option._
 
# Backup
 
For evaluating Confluence you can use the built-in database that will store its files in the Confluence Server home directory. In that case it is sufficient to create a backup archive of the directory on the host that is used as a volume (`/data/confluence` in the example above).
 
Confluence's [automatic backup](https://confluence.atlassian.com/display/DOC/Configuring+Backups) is currently not supported in the Docker setup. You can however use the [Production Backup Strategy](https://confluence.atlassian.com/display/DOC/Production+Backup+Strategy) approach if you're using an external database.
 
Read more about data recovery and backups: [Site Backup and Restore](https://confluence.atlassian.com/display/DOC/Site+Backup+and+Restore)
 
# Versioning
 
The `latest` tag matches the most recent release of Atlassian Confluence Server.
So `atlassian/confluence:latest` will use the newest version of Confluence Server available.
 
Alternatively, you can use a specific minor version of Confluence Server by using a version number
tag: `atlassian/confluence-server:5.10`. This will install the latest `5.10.x` version that
is available.
 
 
# Issue tracker
 
Please raise an
[issue](https://jira.atlassian.com/projects/CONF/issues) if you
encounter any problems with this Dockerfile.