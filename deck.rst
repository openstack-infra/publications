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

* Lost OSIC

Infracloud
----------
.. transition:: pan

.. container:: handout

   Lets focus on the community run aspects rather than the hosting
   aspects.

* Community managed. You too can help us run an OpenStack Cloud
* Running Mitaka
* Deployed with OpenStack Puppet and Ubuntu packaging

Gerrit Upgrade
--------------
.. transition:: pan

* Upgraded from 2.11 to 2.13
* Only two commits diverged from upstream
* Mostly a bug fix update

  * Better memory management
  * UI works better on mobile
  * Votes always show up in event stream

* Stepping stone to Gerrit 2.14/2.15

Zuul v3
-------
.. transition:: pan

* Job definitions are ansible playbooks. Familiar to more people.
* Pre merge testing of most job configs
* Handles per project secrets
* Built in multinode support

  * Zuul talks to all nodes in test environment
  * Can be heterogenous mixture of test nodes

* Presentation on Migration http://bit.ly/2m1dLmq

Zuul v3 Example
---------------
.. transition:: pan

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

The Future
----------
.. transition:: pan

* Potential new clouds in the pipeline
* Gerrit 2.14/2.15

  * New Polygerrit UI
  * Notedb
  * Hashtags
  * ACL'd branch deletion

* Path to Zuul v3 release

  * Dashboard
  * Infra commenting on Github
  * Line comment reporting
  * Diverse Nodepool backends

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
