# docker\_openidm

You can use this image to run OpenIDM 4 in a container.
3 containers are launched when launching this image :
 * A LDAP repository, which is populated with pre-configured data when you launch it for the first time.
 * OpenIDM 4.0, automatically launching when you run the container. It contains a pre-configured connector and pre-configured mappings for the ldap. The goal is to have pre-configured settings to quickly test the functionalities of the product, and to help you make your own configurations. In the future, the goal is to set other pre-configured settings, such as workflows for example. 
* A postgresql database to store OpenIDM data, but the synchro with OpenIDM doesn't work. It seems that the image used has a problem. It has to be fixed in the future versions. 

## Code Status

Version : 0.3

## SOURCES HIERARCHY

> ***docker-compose.yml***
>    Contains the settings to launch the 3 containers : how to build them, which ports to synchronize, which volumes to synchronize, topology of the network, ...
>
> ***openidm***
>    Contains specific files to build the openidm image.
>    openidm.zip contains OpenIDM 4.0. It's unziped each time you build the image. You can replace it by another version of OpenIDM if you want.
>    provisioner.openicf-openldap.json & sync.json contains data used by OpenIDM to synchronize with the LDAP.
>
> ***openidm-openldap***
>    Contains specific files to build the ldap.
>    hierarchy.ldif & population.ldif are files used to populate the LDAP directory. You can change them or add your own files if you want.

## INSTALLING THE IMAGE

 * Copy the files in a directory of your choice.
 * Create a directory to store the ldif files that will populate the LDAP. Just create the repository and add the files in it (you will find them in the openidm-openldap repository). If you add your own ldif files, the openldap image will charge them when building the image. But assume that this installation is optimized for the ldif files provided. If you want to use your own files you could experience problems when launching the synchronization in OpenIDM. You can change the settings directly in OpenIDM or by modifying previously the provisioner.openicf-openldap.json & sync.json files in the openidm repository. You can refer to the OpenIDM doc to modify them.
 * If needed, change the path to your ldif files in the docker-compose.yml file. This is a shared volume between the host and the guest. By default, it's /home/user/share.
 * If you want, you can change the location of the other shared volumes. By default, they are located in /opt/, but feel free to change this. Note that you don't have to create them, they will be automatically created when building the images.
 * Run docker-compose up --build to build and to launch the images.
 * You can now connect to your ldap on the port 389 and on OpenIDM on the port 5050 (feel free to change this in the docker-compoose file).
 * You will see the OpenIDM logs on the prompt.
 * You can stop or destroy your containers by running docker-compose stop or docker-compose down (see man) in another terminal.

## PROBLEMS

The postgresql database image launches but the connection with OpenIDM doesn't work, so it is deactivated for the moment. It seems that the image provided by foregrock doesn't work. OpenIDM also uses an embedded database. This has to be fixed in the next versions.

## Requirements

See the Docker requirements. This image is optimized for Linux distributions (shared volumes).
