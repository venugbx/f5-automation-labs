.. |labmodule| replace:: 1
.. |labnum| replace:: 3
.. |labdot| replace:: |labmodule|\ .\ |labnum|
.. |labund| replace:: |labmodule|\ _\ |labnum|
.. |labname| replace:: Lab\ |labdot|
.. |labnameund| replace:: Lab\ |labund|

Lab |labmodule|\.\ |labnum|\: Connect to f5-super-netops-container
------------------------------------------------------------------

In the previous lab we started the container image and were presented in a
root user terminal.  In order to use the container and its associated
tools properly we will connect via SSH and/or HTTP.

.. _lab1_3_1:

Task 1 - Connect via SSH
~~~~~~~~~~~~~~~~~~~~~~~~

To connect to the image via SSH we must use the published port specified in the
``docker run`` command.  **To review** the command used to start the container was:

**docker run -p 8080:80 -p 2222:22 -p 10000:8080 --rm -it -e SNOPS_GH_BRANCH=master
f5devcentral/f5-super-netops-container:jenkins**

This will publish the standard SSH service from **TCP/22** to **TCP/2222**.
In the case of the SSH service the following mapping applies:

**localhost:2222 -> f5-super-netops-container:22**

Execute below to SSH into the container includes the ``snops`` user with a
password of ``default``.

``ssh -p 2222 snops@localhost``

.. NOTE:: The host SSH keys for our environment are regenerated each time the container boots,
   you may receive an error when trying to connect indicating the host
   key has changed.  This error is safe to ignore in this case and can be
   resolved by removing the key from ``~/.ssh/known_hosts``.  You can also
   configure your local SSH config by adding the following to ``~/.ssh/config``:

   .. code::

       Host localhost
       Port 2222
       StrictHostKeyChecking no
       UserKnownHostsFile /dev/null

Example output of connecting to the container:

.. code::

   $ ssh -p 2222 snops@localhost
   Warning: Permanently added '[localhost]:2222' (ECDSA) to the list of known hosts.
   snops@localhost's password:
                                   .----------.
                                  /          /
                                 /   ______.'
                           _.._ /   /_
                         .' .._/      '''--.
                         | '  '___          `.
                       __| |__    `'.         |
                      |__   __|      )        |
                         | | ......-'        /
                         | | \          _..'`
                         | |  '------'''
                         | |                      _
                         |_|                     | |
    ___ _   _ _ __   ___ _ __          _ __   ___| |_ ___  _ __  ___
   / __| | | | '_ \ / _ \ '__| ______ | '_ \ / _ \ __/ _ \| '_ \/ __|
   \__ \ |_| | |_) |  __/ |   |______|| | | |  __/ || (_) | |_) \__ \
   |___/\__,_| .__/ \___|_|           |_| |_|\___|\__\___/| .__/|___/
             | |                                          | |
             |_|                                          |_|

   Welcome to the f5-super-netops-container.  This image has the following
   services running:

    SSH  tcp/22
    HTTP tcp/80

   To access these services you may need to remap ports on your host to the
   local container using the command:

    docker run -p 8080:80 -p 2222:22 -it f5devcentral/f5-super-netops-container:base

   From the HOST perspective, this results in:

    localhost:2222 -> f5-super-netops-container:22
    localhost:8080 -> f5-super-netops-container:80

   You can then connect using the following:

    HTTP: http://localhost:8080
    SSH:  ssh -p 2222 snops@localhost

   Default Credentials:

    snops/default
    root/default

   Go forth and automate!
   [snops@f5-super-netops] [~] $

Task 2 - Connect via HTTP
~~~~~~~~~~~~~~~~~~~~~~~~~

To connect to the image via HTTP we use the published port specified in the
``docker run`` command.  **To review** the command used to start the container was:

**docker run -p 8080:80 -p 2222:22 -p 10000:8080 --rm -it -e SNOPS_GH_BRANCH=master
f5devcentral/f5-super-netops-container:jenkins**

This will publish the standard HTTP service from **TCP/80** to **TCP/8080**.
In the case of the HTTP service the following mapping applies:

**localhost:8080 -> f5-super-netops-container:80**

Open Chrome on your Linux Jumphost and enter the URL:

``http://localhost:8080/start``

You should see a page like this:

|lab-3-1|

Task 3 - Connect via Jenkins
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To connect to the image via Jenkins we use the published port specified in the
``docker run`` command.  **To review** the command used to start the container was:

**docker run -p 8080:80 -p 2222:22 -p 10000:8080 --rm -it -e SNOPS_GH_BRANCH=master
f5devcentral/f5-super-netops-container:jenkins**

This will publish the standard Jenkins service from **TCP/8080** to **TCP/10000**.
In the case of the Jenkins service the following mapping applies:

**10.1.1.8:10000 -> f5-super-netops-container:8080**

To connect to Jenkins open a web browser and enter the URL:

``http://localhost:10000``

You should see a page like this:

|lab-3-2|

.. |lab-3-1| image:: images/lab-3-1.png
   :align: middle
   :scale: 50%
.. |lab-3-2| image:: images/lab-3-2.png
   :align: middle
   :scale: 95%
