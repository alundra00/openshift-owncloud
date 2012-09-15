ownCloud on OpenShift
======================

This git repository helps you get up and running quickly w/ an owncloud
installation on OpenShift.  The backend database is MySql and the database
name is the same as your application name (using $_ENV['OPENSHIFT_APP_NAME']).
You can name your application whatever you want.  However, the name of the
database will always match the application so you might have to update
.openshift/action_hooks/build.

Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Create a php-5.3 application (you can call your application whatever
you want)

    rhc app create -a cloud -t php-5.4

Add the mysql and phpmyadmin

    rhc app cartridge add -a cloud -c mysql-5.1
    rhc app cartridge add -a cloud -c phpmyadmin-5.4

Add this upstream owncloud repo:

    cd cloud

    # you may need to remove index.php
    git rm php/index.php
    git commit -a

    git remote add upstream -m master git://github.com/dyfet/openshift-owncloud.git
    git pull -s recursive -X theirs upstream master
    # note that the git pull above can be used later to pull updates to
    # Etherpad the rm and ln is there until I can figure out github and
    # symbolic links
Then push the repo upstream

    git push

You can now login to your owncloud instance and go through it's initial
setup.  You should create your initial user with your own user id and password
and select "mysql" from the owncloud initial login and setup.  You can enter
your mysql db credentials.  Thats it, owncloud is then up and running!

