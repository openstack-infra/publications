::

  This work is licensed under a Creative Commons Attribution 3.0
  Unported License.
  http://creativecommons.org/licenses/by/3.0/legalcode

===============================
 Infrastructure Project Update
===============================

Blank Slide
-----------
.. hidetitle::

Main Title
----------
.. transition:: tilt
   :duration: 2
.. hidetitle::
.. figlet:: An Important News Update

An OpenStack Infrastructure Team Production

Gerrit Upgrade
--------------

TODO

Meltdown / Spectre
------------------

TODO

State of the Clouds
-------------------
.. transition:: tilt
   :duration: 2

* Thank you to all our infra resource donors!
* Current Clouds (in alpha order)

  * Citycloud
  * Infracloud
  * Internap
  * OVH
  * Rackspace
  * Vexxhost
  * TODO: arm

Lost infra-cloud

Zuul v3 Deployed
----------------
.. transition:: pan

TODO

Zuul v3 Secrets
---------------
.. transition:: pan

TODO talk about how secrets work (we've never had anything like this).

Zuul v3 Branches
---------------
.. transition:: pan

TODO talk about branch matchers, etc.

Zuul v3 GitHub
--------------
.. transition:: pan

TODO talk about reporting on GitHub and other projects

Zuul v3 Job Migration
---------------------
.. transition:: pan

TODO talk about how people should migrate (highlight major changes to the zuulv3 infra-manual page since the initial publication)

Zuul v3 Devstack
----------------
.. transition:: pan

TODO update

.. code:: yaml

  - job:
      name: devstack
      parent: multinode
      description: Base devstack job
      nodeset: openstack-single-node
      required-projects:
        - openstack-dev/devstack
        - openstack/cinder
        - openstack/glance
        - openstack/keystone
        - openstack/neutron
        - openstack/nova
        - openstack/requirements
        - openstack/swift
      roles:
        - zuul: openstack-infra/openstack-zuul-jobs
      pre-run: playbooks/pre.yaml
      run: playbooks/devstack.yaml
      post-run: playbooks/post.yaml
      vars:
        devstack_localrc:
          ADMIN_PASSWORD: secretadmin
        devstack_services:
          horizon: False
          tempest: False

Zuul v3 Tempest
---------------
.. transition:: pan

TODO

TC Top 5 Help Wanted
--------------------
.. transition:: pan

* Community Infrastructure Sysadmins

  * https://governance.openstack.org/tc/reference/top-5-help-wanted.html

Contact Info
------------
.. transition:: pan

* IRC: #openstack-infra on Freenode
* E-mail: openstack-infra@lists.openstack.org
* In person: https://www.openstack.org/ptg/
* Documentation: https://docs.openstack.org/infra/system-config/
* ...and all around the Forum -- feel free to say hi!

Questions
---------
.. transition:: tilt
   :duration: 2
.. hidetitle::
.. figlet:: Questions?
