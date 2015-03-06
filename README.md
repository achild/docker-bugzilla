## docker-bugzilla

Run a docker container for Bugzilla.  The image will install apache2/bugzilla/msmtp and setup bugzilla to run as localhost.  It will remove the default localhost (html) and create a symbolic link to /var/www/html for bugzilla.  The dockerfile will disable the default and enable the bugzilla.conf which is included. It will also enable cgi, headers, and expires and a start script that will run the final ./checksetup/pl to complete the installation.  

### start script

You can uncomment any of the DEFAULT variables and the sed execution to simply substitute values via the command line during docker run.  By default apache runs as apache so you can change ownership to apache to use the DEFAULT variable to set the group and owner to www-data.

### Usage

For my case I am upgrading and existing installation of bugzilla and I am passing in three different conf files at run time using a -v option.  For most cases you can use pass in various environment varibles.

> docker run -d -p 80:80 --name bugzilla \
>-v /tmp/msmtprc:/etc/msmtprc:ro \
>-e MYSQL_DB=<database> -e MYSQL_USER=<user> \
>-e MYSQL_PWD=<password> achild/bugzilla