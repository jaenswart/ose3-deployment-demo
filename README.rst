======
README
======


Overview
========

The purpose of this project is to document and demonstrate an OSE 3.2
deployment in an HA configuration using an OpenStack cloud provider.

Now there are a couple ways of using this document. One way is to read through
it, and follow the examples step by step. The *other* way is to run it, and let
the examples deploy OSE for you, automatically.

Yes, that's right. This is an executable document, and it can build your whole
OSE3 environment for you! Pretty cool, huh? There's a little setup involved,
covered below.


Requirements
============


System Requirements
-------------------

Python 2.7 or higher is required to build the documentation and run the
examples.

This project has been tested on Fedora 23, but should work on other flavors of
Red Hat Linux.

On recent versions of Fedora, these can be installed using:

.. code-block:: shell

    # dnf install python python-virtualenv redhat-rpm-config openssl-devel git

On RHEL or older versions of Fedora, install by running:

.. code-block:: shell

    # yum install python python-virtualenv redhat-rpm-config openssl-devel git

If you simply wish to read the documentation without fancy rendering or running
the examples, only a basic text editor is required.


RHN
---

An active RHN login is required and you need available subscriptions for RHEL7
and OSE3.2 repositories.


OS1/OpenStack
-------------

An active OpenStack login is required in OS1 Public (other OpenStack
environments may work too, but are untested). You need permissions to manage
instances, volumes, images, floating IPs, SSH keys, and security groups.

OS1 Public is the targeted OpenStack cloud platform, and this project has only
been tested against that environment. Other OpenStack environments will likely
work too, but may require minor modifications.


Installation
============

To build documentation and run the examples, the following Python packages are
installed:

- Ansible
- OpenStack Client
- Shade
- Sphinx

If you haven't done so already, now would be a good time to check out the code.

.. code-block:: shell

    $ git clone https://github.com/ajsmith/ose3-deployment-demo.git
    $ cd ose3-deployment-demo

Follow the steps below to perform the installation:

*Note: Installation does not require root privileges.*

.. code-block:: shell

    $ virtualenv ~/py
    $ source ~/py/bin/activate
    $ pip install -r requirements.txt


Building the Documentation
==========================

To build the HTML documentation, do the following:

.. code-block:: shell

    $ source ~/py/bin/activate
    $ make html

The rendered documentation can now be found in `_build/html/`.

Or to render as a PDF, do:

.. code-block:: shell

    $ source ~/py/bin/activate
    $ make latexpdf

*Note: Additional texlive packages may need to be installed for PDF
generation.*


Demo
====

The documentation presented here isn't just for reading. You can run it too!
Running this document will demonstrate the full OSE3 deployment. Aside from a
few manual steps to setup your environment, the deployment is fully automated.

To tell which steps are manual and which are executed:

- Examples prefixed with ">>>" are executable and will be run as part of the
  demo.

- Shell instructions (prefixed with "$" or "#") are *not* executable and must
  be performed manually.


OpenStack Setup
---------------

Running the examples depend on your environment being set up to authenticate
with an OpenStack environment. You will need to download your "openrc.sh" file
from the OpenStack dashboard. To do so:

#. Sign in to the OpenStack Dashboard
#. Go to the "Access & Security" page
#. Click on the "API Access" tab
#. Click the "Download OpenStack RC File" button

Once you've downloaded your RC file, add to your environment:

.. code-block:: shell

    $ source myproject-openrc.sh

You'll also need to configure some Ansible variables to match your specific
environment. These settings are configured in 'ansible/vars/openstack.yaml'. An
example file lives in the same directory (named 'openstack.yaml.example') which
you can copy and customize.

.. literalinclude:: ansible/vars/openstack.yaml.example
   :caption:
   :language: yaml


RHN Setup
---------

RHN registration information needs to be configured in order to update RHEL and
install OSE packages. A username, password, and a pool ID must be
provided. These settings are configured in
'ansible/roles/rhn/vars/main.yaml'. An example file lives in the same directory
(named 'main.yaml.example') which you can copy and customize.

.. literalinclude:: ansible/roles/rhn/vars/main.yaml.example
   :caption:
   :language: yaml


Running the Demo
----------------

Once you've performed the installation and environment setup steps above,
you'll be ready to run the demo!

To run the thing, do:

.. code-block:: shell

    $ source ~/py/bin/activate
    $ make doctest

Keep in mind this demo sets up an entire OSE environment from scratch and as
such can take a very long time to run (perhaps hours). Still, it beats typing,
so grab some coffee, sit back, and enjoy the show!
