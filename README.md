# docker\_openidm

You can use this image to run OpenIDM 4 in a container.
4 containers are launched when launching this image :
 * A LDAP repository, which is populated with pre-configured data when you launch it for the first time.
 * OpenIDM 4.0, automatically launching when you run the container. It contains a pre-configured connector and pre-configured mappings for the ldap. The goal is to have pre-configured settings to quickly test the functionalities of the product, and to help you make your own configurations. In the future, the goal is to set other pre-configured settings, such as workflows for example. 
 * A postgresql database to store OpenIDM data.
 * A webserver with phppgadmin to administrate it.

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
>
> ***openidm-phppgadmin***
>    Contains specific files to build phppgadmin. It is similar to the jacksoncage/phppgadmin image on docker hub but we added some fixes.

## INSTALLING THE IMAGE

 * Copy the files in a directory of your choice.
 * You have to create two directories : one for the ldif files needed to populate the LDAP server, and one for custom files for OpenIDM. By default, the paths are :
       /home/user/share/ldapprepopulate for openldap
       /home/user/share/openidmcustom   for openidm
 You can use the location you want, in this case just make sure to change the path in the docker-compose file, in the "shared volumes" section.
 * Copy the requiered files to these directories :
       For openldap : the ldif files which you can find in openidm-openldap/ (1)
       For openidm  : the datasource.jdbc-default.json, logging.properties, repo.jdbc.json files which you can find in /openidm. If you don't copy them, the synchro with the databse will not work.
 * There are other shared volumes, but you don't have to create them, they will be automatically created when building the images. If you want, you can change the location of the other shared volumes. By default, they are located in /opt/, but feel free to change this.
 * Run docker-compose up --build to build and to launch the images.
 * You can now connect to your ldap on the port 389, on OpenIDM on the port 8080 and on the webserver on the port 8000 (feel free to change this in the docker-compoose file).
 * You will see the OpenIDM logs on the prompt.
 * You can stop or destroy your containers by running docker-compose stop or docker-compose down (see man) in another terminal.

(1) You can add your own ldif files, the openldap image will charge them when building the image. But assume that this installation is optimized for the ldif files provided. If you want to use your own files you could experience problems when launching the synchronization in OpenIDM. You can change the settings directly in OpenIDM or by modifying previously the provisioner.openicf-openldap.json & sync.json files in the openidm repository. You can refer to the OpenIDM doc to modify them.
 
## PROBLEMS

Tested on debian jessie and did work properly.

## Requirements

See the Docker requirements. This image is optimized for Linux distributions (shared volumes).
