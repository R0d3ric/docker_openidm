# R0d3ric/docker\_openidm

You can use this image to run OpenIDM 4 in a container.
3 containers are launched when launching this image :
 * A LDAP repository, which is populated with preconfigured data when you launch it for the first time.
 * OpenIDM 4.0, automatically launching when you run the container. It contains a pre-configured connector and pre-configured mappings for the ldap. The goal is to have pre-configured settings to quickly test the fonctionnalities of the product, and to help you making your own configurations. In the future, the goal is to set other pre-configured settings, such as workflows for example.
 * A plsql database for OpenIDM, but the synchro with OpenIDM doesn't work. It seems that the image used has a problem. It has to be fixed in the future versions.

## Code Status

Version : 0.2

## SOURCES HIERARCHY

> TODO

## INSTALLING THE IMAGE

TODO

## PROBLEMS

## Requirements

See the Docker requirements. This image is optimised for Linux distributions (shared volumes).
