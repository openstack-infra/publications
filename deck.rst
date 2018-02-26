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

* Gerrit upgraded to 2.13

  * Many bugfixes
  * You can now repush old patchsets

* Plan to upgrade to 2.14.

Meltdown / Spectre
------------------

* Infra services patched against Meltdown

  * Xen largely avoided this at hypervisor level

* Retpoline showing up to address part of Spectre

  * Performance degradation using UCA qemu post Spectre mitigation
  * Rely on cloud providers to update hardware

State of the Clouds
-------------------
.. transition:: tilt
   :duration: 2

* Thank you to all our infra resource donors!
* Current Clouds (in alpha order)

  * Citycloud
  * Internap
  * Linaro (in progress)
  * OVH
  * Rackspace
  * Vexxhost

* No more Infracloud

Zuul v3 Deployed
----------------
.. transition:: dissolve
.. hidetitle::

.. ansi:: zuul.ans


Zuul v3 Secrets
---------------
.. transition:: pan

.. code-block::

   - secret:
       name: kolla_dockerhub_creds
       data:
         password: !encrypted/pkcs1-oaep
           - QLe52Ymma5HJg3K2kgeSEMp7TwarkH8AbEiwcnDTqZ276BUF9wrt+5gPJRfVU1BYty2lq
             CCzhawJJ09TV0WU2SEUKlicWoXQ/hcbYWNlOHVL6/gm9UxZP/GC8d1eyQfbCS7UUHfiHF
             BLAHBLAHBLAHBLAHBLAH=

   - job:
       name: kolla-publish-ubuntu-binary
       post-run: tests/playbooks/publish.yml
       secrets:
         - kolla_dockerhub_creds

   - hosts: all
     tasks:
       - name: Login to Dockerhub
         command: "docker login -u {{ kolla_dockerhub_creds.user }} -p {{ kolla_dockerhub_creds.password }}"
         no_log: true

       - shell: "for img in $(docker images  --format '{% raw %}{{ .Repository }}:{{ .Tag }}{% endraw %}' | grep kolla ); do docker push $img; done"


Zuul v3 Branches
---------------
.. transition:: pan

* Jobs in branched repos get *implied branch matchers*
* Jobs in branchless repos have no implied branch matchers
* Any job can set *explicit branch matchers*
* We're backporting some jobs to stable branches now
* In the future, branching should just DTRT
  
Zuul v3 GitHub
--------------
.. transition:: pan

* OpenStack's Zuul can report on projects on GitHub now
* https://github.com/ansible/ansible/pull/20974
* Pending TC resolution and docs changes describing process

Zuul v3 Job Docs
----------------
.. transition:: pan

* Zuul-sphinx plugin
* https://docs.openstack.org/infra/zuul-jobs/
* https://docs.openstack.org/infra/openstack-zuul-jobs/
* https://docs.openstack.org/infra/zuul/user/config.html

Zuul v3 Job Migration
---------------------
.. transition:: pan

* Auto-migrated jobs start with `legacy-`
* Migrate those out of openstack-zuul-jobs into your own repos
* Look into whether existing Ansible roles are useful, or if the jobs or roles
  that you develop may be generally useful
* https://docs.openstack.org/infra/manual/zuulv3.html

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

* https://governance.openstack.org/tc/reference/
  top-5-help-wanted.html

Contact Info
------------
.. transition:: pan

* IRC: #openstack-infra on Freenode
* E-mail: openstack-infra@lists.openstack.org
* In person: https://www.openstack.org/ptg/

  * Infra help room: *Davin Suite, L4*
  
* Documentation: https://docs.openstack.org/infra/system-config/
* ...and all around the PTG -- feel free to say hi!

Questions
---------
.. transition:: tilt
   :duration: 2
.. hidetitle::
.. figlet:: Questions?
