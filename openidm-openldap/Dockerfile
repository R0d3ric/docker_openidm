FROM dinkel/openldap:latest

MAINTAINER roderic.halleguen@capgemini.com

RUN apt-get update && apt-get install ldap-utils --assume-yes \
 && rm -rf /var/lib/apt/lists/*

#RUN apt-get upgrade

#ADD hierarchy.ldif /etc/ldap.dist/prepopulate/hierarchy.ldif

#ADD population.ldif /etc/ldap.dist/prepopulate/population.ldif

#RUN ldapadd -x -h localhost -D cn=admin,dc=cybersecu,dc=cap -w password -f /etc/ldap.dist/prepopulate/hierarchy.ldif -d1
#RUN ldapadd -x -h 'cn=admin,dc=cybersecu,dc=cap' -w password -f /etc/ldap.dist/prepopulate/hierarchy.ldif
#RUN ldapadd -x -D 'cn=admin,dc=cybersecu,dc=cap' -w password -f /etc/ldap.dist/prepopulate/population.ldif
