Use of OpenStack CI for your own projects
=========================================

A tour of the CI automation process used for OpenStack, focusing technically on
all the components used to compose the full CI workflow, and exposing how they
are interrelated and how the whole process is automated.

This slide deck is a general overview of all components related into Openstack
CI process:

* Gerrit and git review for code submission
* Zuul for dealing with branches and merges
* Jenkins to execute tests and related jobs such as building tarballs,
  documentation or packagesa
* Nodepool for dealing with resources needed to execute all testing

