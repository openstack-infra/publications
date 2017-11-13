::

  This work is licensed under a Creative Commons Attribution 3.0
  Unported License.
  http://creativecommons.org/licenses/by/3.0/legalcode

Migrating your job from Jenkins Job Builder to Ansible Playbooks
================================================================
.. cowsay:: A Zuulv3 Story
.. transition:: tilt

Who am I?
=========
.. container:: progressive
.. transition:: tilt

Paul Belanger

 - OpenStack Project Infrastructure Core
 - irc: pabelanger
 - twitter: @pabelanger

What are we going to talk about?
================================
.. transition:: tilt

`Jenkins Job Builder (JJB)`

 - Tools to make Jenkins jobs from templates
 - Written in YAML or JSON
 - Human readable text format
 - Store in version control system
 - Easy to make changes; code review
 - Flexible template system

What are we going to talk about?
================================
.. transition:: tilt
.. container:: progressive

`Ansible`

 - Simple / powerful IT automation
 - Written in YAML or JSON
 - Human readable text format
 - Store in version control system
 - Easy to make changes; code review
 - Flexible template system

There is no Jenkins, only Zuul!
===============================
.. transition:: tilt

An effort to streamline Zuul and Nodepool into an easier-to-user system that
scales better and is more flexible:

  - Make zuul scale to thousands of projects.
  - Make Zuul more multi-tenant friendly.
  - Make it easier to express complex scenarios in layout.
  - Make nodepool more useful for non virtual nodes.
  - Make nodepool more efficient for multi-node tests.
  - Remove need for long-running slaves.
  - Make it easier to use Zuul for continuous deployment.
  - Support private installations using external test resources.
  - Keep zuul simple.

https://specs.openstack.org/openstack-infra/infra-specs/specs/zuulv3.html

Zuulv3 Overview
===============
.. transition:: tilt
.. graphviz::
   :align: center

   graph  {
      node [shape=box]
      Gearman [shape=ellipse]
      Gerrit [fontcolor=grey]
      Zookeeper [shape=ellipse]
      Nodepool
      GitHub [fontcolor=grey]

      Merger -- Gearman
      Executor -- Gearman
      Web -- Gearman

      Gearman -- Scheduler;
      Scheduler -- Gerrit;
      Scheduler -- Zookeeper;
      Zookeeper -- Nodepool;
      Scheduler -- GitHub;
   }

JJB: Installation
=================
.. transition:: tilt
.. code-block::

    $ virtualenv jjb-env
    $ source jjb-env/bin/activate
    $ pip install jenkins-job-builder

JJB: Hello World
================
.. transition:: tilt
.. code-block::

    $ cat jjb/hello-world.yaml
    - job:
        name: hello-world
        description: Example hello world job
        builders:
          - shell: |
              #!/bin/sh
              echo 'hello world'

JJB: Testing
============
.. transition:: tilt
.. code-block::

    $ jenkins-jobs test jjb/hello-world.yaml
    INFO:root:Will use anonymous access to Jenkins if needed.
    INFO:jenkins_jobs.builder:Number of jobs generated:  1
    INFO:jenkins_jobs.builder:Job name:  hello-world
    <?xml version="1.0" encoding="utf-8"?>
    <project>
      <actions/>
      <description>Example hello world job&lt;!-- Managed by Jenkins Job Builder --&gt;</description>
      <keepDependencies>false</keepDependencies>
      <blockBuildWhenDownstreamBuilding>false</blockBuildWhenDownstreamBuilding>
      <blockBuildWhenUpstreamBuilding>false</blockBuildWhenUpstreamBuilding>
      <concurrentBuild>false</concurrentBuild>
      <canRoam>true</canRoam>
      <properties/>
      <scm class="hudson.scm.NullSCM"/>
      <builders>
        <hudson.tasks.Shell>
          <command>#!/bin/sh
    echo 'hello world'
    </command>
        </hudson.tasks.Shell>
      </builders>
      <publishers/>
      <buildWrappers/>
    </project>

JJB: Recap
==========
.. transition:: tilt

For a long time, this is how we deal with job configuration in the OpenStack
project.

Pros:

 - No longer edit jobs in GUI
 - scales
 - version control
 - code review
 - validate job syntax

Cons:

 - Difficult to test jobs
 - Need external jenkins server, if we wanted too
 - Additional (testing) code to maintain
 - Converted to XML, another layer to debug

Ansible: Installation
=====================
.. transition:: tilt
.. code-block::

    $ virtualenv ansible-env
    $ source ansible-env/bin/activate
    $ pip install ansible

Ansible: Hello World
================
.. transition:: tilt
.. code-block::

    $ cat playbooks/hello-world/run.yaml
    - hosts: all
      tasks:
        - name: Print hello world
          command: echo 'hello world'
          changed_when: True

Ansible: Checking Syntax
============
.. transition:: tilt
.. code-block::

    $ ansible-playbook -i tests/inventory --check-syntax playbooks/hello-world/run.yaml
    playbook: playbooks/hello-world/run.yaml

Ansible: Linting
============
.. transition:: tilt
.. code-block::

    $ pip install ansible-lint
    $ ansible-lint playbooks/hello-world/run.yaml
    $ echo $?
    0

Ansible: Testing
============
.. transition:: tilt
.. code-block::

    $ ansible-playbook -i tests/inventory playbooks/hello-world/run.yaml
    PLAY [all] ****************************************************************

    TASK [Gathering Facts] ****************************************************
    ok: [localhost]

    TASK [Print hello world] **************************************************
    changed: [localhost]

    PLAY RECAP ****************************************************************
    localhost                  : ok=2    changed=1    unreachable=0    failed=0

Ansible: Recap
==============
.. transition:: tilt

More power in the hands of developers:

Pros:

 - scales
 - version control
 - code review
 - syntax-check / linting of playbooks
 - No external service, can test locally
 - Use production playbooks

Cons:

 - Upgrades of ansible can break playbooks
 - If you are not using ansible, another thing to learn
 - Can't really think of anything

Zuulv3: configuration
=====================
.. transition:: tilt
.. code-block::

    $ cat .zuul.yaml
    - job:
        name: sandbox-hello-world
        description: Simple hello world job.
        run: playbooks/hello-world/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - project:
        name: openstack-dev/sandbox
        check:
          jobs:
            - sandbox-hello-world
        gate:
          jobs:
            - sandbox-hello-world

Zuulv3: Results
===============
.. transition:: tilt
.. code-block::

    RUN START: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/hello-world/run.yaml@master]

    PLAY [all]

    TASK [Print hello world]
    controller | hello world
    controller | ok: Runtime: 0:00:00.003554

    PLAY RECAP
    controller | ok: 1 changed: 1 unreachable: 0 failed: 0

    RUN END RESULT_NORMAL: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/hello-world/run.yaml@master]

Zuulv3: Acheivement Unlocked
============================
.. transition:: tilt

We took hello-world playbook and ran it both locally (localhost) and remote node
(controller).  We didn't need to make any changes to our job, we just told Zuul
how we wanted it to be ran.

Lets start adding more coverage to our playbooks.

Zuulv3: ansible-lint
====================
.. transition:: tilt
.. code-block::

    $ cat playbooks/ansible-lint/pre.yaml
    - hosts: all
      tasks:
        - name: Install ansible-lint via pip
          pip:
            name: ansible-lint
            extra_args: --user

    $ cat playbooks/ansible-lint/run.yaml
    - hosts: all
      tasks:
        - name: Check linting of playbooks
          shell: ~/.local/bin/ansible-lint playbooks/*/*.yaml
          args:
            chdir: "{{ zuul.project.src_dir }}"
          changed_when: True

Zuulv3: configuration
=====================
.. transition:: tilt
.. code-block::

    $ cat .zuul.yaml
    - job:
        name: sandbox-ansible-lint
        description: Example ansible-lint job.
        pre-run: playbooks/ansible-lint/pre.yaml
        run: playbooks/ansible-lint/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - job:
        name: sandbox-hello-world
        description: Simple hello world job.
        run: playbooks/hello-world/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - project:
        name: openstack-dev/sandbox
        check:
          jobs:
            - sandbox-ansible-lint
            - sandbox-hello-world
        gate:
          jobs:
            - sandbox-ansible-lint
            - sandbox-hello-world

Zuulv3: Results
===============
.. transition:: tilt
.. code-block::

    PRE-RUN START: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-lint/pre.yaml@master]

    PLAY [all]

    TASK [Install ansible-lint via pip]
    controller | changed

    PLAY RECAP
    controller | ok: 1 changed: 1 unreachable: 0 failed: 0

    PRE-RUN END RESULT_NORMAL: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-lint/pre.yaml@master]
    RUN START: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-lint/run.yaml@master]

    PLAY [all]

    TASK [Check linting of playbooks]
    controller | ok: Runtime: 0:00:01.010124

    PLAY RECAP
    controller | ok: 1 changed: 1 unreachable: 0 failed: 0

    RUN END RESULT_NORMAL: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-lint/run.yaml@master]


Zuulv3: ansible-playbook --syntax-check
=======================================
.. transition:: tilt
.. code-block::

    $ cat playbooks/ansible-syntax/pre.yaml
    - hosts: all
      tasks:
        - name: Install ansible via pip
          pip:
            name: ansible
            extra_args: --user

    $ cat playbooks/ansible-syntax/run.yaml
    - hosts: all
      tasks:
        - name: Check syntax of playbooks
          shell: ~/.local/bin/ansible-playbook -i tests/inventory --syntax-check playbooks/*/*.yaml
          args:
            chdir: "{{ zuul.project.src_dir }}"
          changed_when: True

Zuulv3: configuration
=====================
.. transition:: tilt
.. code-block::

    $ cat .zuul.yaml
    - job:
        name: sandbox-ansible-lint
        description: Example ansible-lint job.
        pre-run: playbooks/ansible-lint/pre.yaml
        run: playbooks/ansible-lint/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - job:
        name: sandbox-ansible-syntax
        description: Example ansible-syntax job.
        pre-run: playbooks/ansible-syntax/pre.yaml
        run: playbooks/ansible-syntax/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - job:
        name: sandbox-hello-world
        description: Simple hello world job.
        run: playbooks/hello-world/run.yaml
        nodesets:
          nodes:
            - name: controller
              label: ubuntu-xenial

    - project:
        name: openstack-dev/sandbox
        check:
          jobs:
            - sandbox-ansible-lint
            - sandbox-ansible-syntax
            - sandbox-hello-world
        gate:
          jobs:
            - sandbox-ansible-lint
            - sandbox-ansible-syntax
            - sandbox-hello-world

Zuulv3: Results
===============
.. transition:: tilt
.. code-block::

    PRE-RUN START: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-syntax/pre.yaml@master]

    PLAY [all]

    TASK [Install ansible via pip]
    controller | changed

    PLAY RECAP
    controller | ok: 1 changed: 1 unreachable: 0 failed: 0

    PRE-RUN END RESULT_NORMAL: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-syntax/pre.yaml@master]
    RUN START: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-syntax/run.yaml@master]

    PLAY [all]

    TASK [Check syntax of playbooks]
    controller |
    controller | playbook: playbooks/ansible-syntax/pre.yaml
    controller |
    controller | playbook: playbooks/ansible-syntax/run.yaml
    controller |
    controller | playbook: playbooks/hello-world/run.yaml
    controller | ok: Runtime: 0:00:01.059858

    PLAY RECAP
    controller | ok: 1 changed: 1 unreachable: 0 failed: 0

    RUN END RESULT_NORMAL: [untrusted : git.openstack.org/openstack-dev/sandbox/playbooks/ansible-syntax/run.yaml@master]

Zuul Jobs
=========
.. transition:: tilt

What else have we done?
 - build-javascript-tarball
 - python-sdist
 - tox
 - tox-docs
 - tox-py27

https://docs.openstack.org/infra/zuul-jobs/

More Information
================
.. transition:: tilt

- IRC: #zuul on Freenode
- Mailing List: https://lists.openstack.org/pipermail/openstack-infra/
- Documentation: https://docs.openstack.org/infra/zuul/
- Source:

  - https://git.openstack.org/cgit/openstack-infra/openstack-zuul-jobs
  - https://git.openstack.org/cgit/openstack-infra/zuul
  - https://git.openstack.org/cgit/openstack-infra/zuul-jobs

Questions?
==========
.. transition:: tilt
.. hidetitle::
.. container:: handout
.. figlet:: Questions?
