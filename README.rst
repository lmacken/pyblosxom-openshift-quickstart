Blogging with PyBlosxom in the Red Hat Cloud with OpenShift Express
===================================================================

PyBlosxom is a lightweight file-based weblog system. PyBlosxom focuses on
three things: simplicity, extensibility, and community.

    http://pyblosxom.bluesock.org

* simplicity - PyBlosxom uses the file system for all its data storage. Because of this you can use whatever existing editor, scripts and tools you want to create, update and manipulate entries and other blog data.
* extensibility - PyBlosxom has a plugin framework allowing you to build plugins in Python to augment and change PyBlosxom's default behavior.
* community - There are hundreds of PyBlosxom users out there all of whom have different needs. PyBlosxom is used on a variety of operating systems in a variety of environments. The pyblosxom users list shares their experiences, plugins, and expertise. The pyblosxom devel list shares their ideas for changes, patches and plugins.

Get started with OpenShift Express
----------------------------------

* Create an account at http://openshift.redhat.com
* Install the rhc package and create your domain

The easy way
------------

You can easily deploy a PyBlosxom blog to the OpenShift cloud with a single command, using my `openshift-quickstarter` tool: http://github.com/lmacken/openshift-quickstarter

::

    ./openshift-quickstarter EMAIL DOMAIN APPNAME pyblosxom

That's it! You can now view your blog at:

::

    http://APPNAME-DOMAIN.rhcloud.com

.. image:: http://lewk.org/img/pyblosxom-quickstart.png


The scenic route
----------------

If you don't want to use the `openshift-quickstarter`, you can easily create a new OpenShift WSGI application and merge this quickstart into it manually:

::

    rhc-create-app -a tg2 -t wsgi-3.2 -l your@email.com
    rhc-ctl-app -a tg2 -e add-mysql-5.1 -l your@email.com
    cd tg2app
    git remote add upstream -m master git://github.com/lmacken/pyblosxom-openshift-quickstart.git
    git pull -s recursive -X theirs upstream master
    git push

Monitoring your logs
--------------------

::

    rhc-tail-files -a tg2app -l your@email.com
