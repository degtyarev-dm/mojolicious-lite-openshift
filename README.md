Mojolicious::Lite on OpenShift
===================

This git repository helps you get up and running quickly w/ a Mojolicious::Lite installation
on OpenShift.  You can feel free to change it.


Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a perl-5.10 application

    rhc app create -a mojolite -t perl-5.10

Add this upstream mojolite repo

    cd mojolite
    git rm -r perl
    git commit -a -m "remove stock perl dir to prepare for Mojolicius::Lite"
    git remote add upstream -m master git://github.com/degtyarev-dm/mojolicious-lite-openshift.git
    git pull -s recursive -X theirs upstream master
    
Change _REPO_DIR_ to the content of $OPENSHIFT_REPO_DIR variable in .htaccess file. You can get something like this

    PerlSetVar psgi_app /var/lib/openshift/____ID____/app-root/runtime/repo/perl/index.pl

Where ____ID____ is your 32-character project id.

Then push the repo upstream

    git push

That's it, you can now checkout your application at:

    http://mojolite-$yournamespace.rhcloud.com