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
* Rocky Cycle Clouds (in alpha order)

  * Arm CI Cloud
  * Internap
  * Limestone Networks
  * Linaro
  * OVH
  * Packethost + Platform9
  * Rackspace
  * Vexxhost

Arm64
-----
.. transition:: tilt

* Added Arm CI Cloud
* Added second Linaro Cloud region
* Total of 3 arm64 cloud regions

Modernizing Config Management
-----------------------------
.. transition:: tilt

* Migrating away from Puppet

  * Puppet 3 to 4 to 5 transition is costly

* Interest of team have shifted to other tools
* Convert to Ansible for config management
* Use containers for "packaging"
* Bastion host and DNS servers now running without puppet
* Complete transition will take time

  * Puppet 4 work being done for some services

Zuul
----
.. transition:: tilt
.. hidetitle::

.. ansi:: zuul.ans

Working Together
----------------
.. transition:: pan

* Zuul now an independent top level project
* Significant overlap in teams

  * Zuul and Infra growing independently too

* Infra and OpenStack act as beta testers for Zuul

  * If it works for us, it will probably work for you too

In Project Configs
------------------
.. transition:: pan

* OpenStack has moved majority of configs into project repos
* Simplifies python3 first transition in OpenStack
* Allows for pre merge testing of in repo job configs
* Infra no longer blocker on most job config changes
* Branchless jobs still in Infra configs

Top Level Project Hosting
-------------------------
.. transition:: tilt

* Modifications made to host different top level projects

  * Mailing list hosting
  * Web hosting
  * Documentation hosting
  * Git repo hosting

* Now hosting tools for Airship, Kata, StarlingX, and Zuul.

OpenDev
-------
.. transition:: pan

* Neutral name to host top level projects under
* Be more welcoming to projects that are not "OpenStack"
* Support broader FOSS ecosystem if projects find our tools useful
* Slow iterative transition

  * Expect a service or two to be renamed at a time

* OpenStack not going anywhere. Still our biggest user.

Looking Ahead
-------------
.. transition:: tilt

* Continue with Modernizing Config Management
* Gerrit 2.15
* Improvements to IRC bot systems
* OpenDev

Contact Info
------------
.. transition:: tilt

* IRC: #openstack-infra on Freenode
* E-mail: openstack-infra@lists.openstack.org
* Here at the Summit
* Documentation: https://docs.openstack.org/infra/system-config/

Questions
---------
.. transition:: tilt
   :duration: 2
.. hidetitle::
.. figlet:: Questions?
