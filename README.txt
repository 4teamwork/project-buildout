Plone project buildout
======================

This buildout is meant to be used as a template for all Plone project
buildouts by 4teamwork.


Usage
-----

We use the same buildout for development and production setups.

No ``buildout.cfg`` file is supplied und should never be added to the
repository. Instead either create a symbolic link to an appropriate
configuration file (e.g. ``development.cfg`` or ``production.cfg``) or extend
a configuration if you intend to make some customizations for your personal
usage only.

Example::

 [buildout]
 extends = development.cfg

 [instance1]
 eggs +=
     Products.PDBDebugMode
     plone.reload
     mr.freeze


Versions
--------

All product versions must be specified in the ``versions.cfg`` file by either
extending a known-good-set (KGS) or by providing the version pinnings in the
file itself. Version pinnings should always be sorted alphabetically and are
split up in three parts:

- Overrides: Contains version pinnings that override pinnings in an included
  KGS.

- Buildout: Contains version pinnings for products related to buildout
  (e.g. recipes).

- Add-ons: Contains version pinnings for Plone add-on products.

The production buildout does not allow any unpinned versions
(``allow-picked-versions=false``).


Sources
-------

All source checkouts must be specified in the ``sources.cfg`` file. For Github
checkouts the pull url should be public while the additionally given push
url (``pushurl`` option) should provide write access. This allows people
without write access for some repos to use the same buildout.

Sources should be sorted alphabetically and may be grouped in sections.


Filestorage
-----------

Each Plone site should be created in a separate filestorage, which is setup
in the ``filestorage`` part in ``base.cfg``. This allows easy moving of
filestorages between Zope instances.


Production Configurations
-------------------------

Specific production configurations should extend ``production.cfg`` and must
always be added to version control.

Use the following name schema: ``production-<servername>-<instance>.cfg`` (e.g.
``production-gamma-02.cfg``)


Supervisor
----------

Production buildouts must always use supervisor, even when using just one Zope
instance.

Supervisor is configured to monitor memory usage of all processes and HTTP
responses of Zope instances.


Post-deployment
---------------

Production buildouts include a ``deployment`` part which does some important
post-deployment configuration. This includes the generation of logrotate
configuration files and run-control scripts for automatic startup.


Contributors
------------

- Thomas Buchberger [buchi], Author
