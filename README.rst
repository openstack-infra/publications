How OpenStack Improves Code Quality with Project Gating and Zuul
================================================================

Abstract
--------

The OpenStack project uses project gating to ensure that the latest
code in the repository always works.  Gating is a process where every
change, after passing code review, is automatically tested and merged
only if it passes the test suite.  Especially for large projects with
complex test suites, this process can keep code quality high while
making it easier to accept patches from new contributors.

The OpenStack Project Infrastructure team developed Zuul to manage its
project gating system.  Zuul is a flexible, general purpose system to
integrate Gerrit code review and Jenkins and can be used for project
automation purposes beyond trunk gating.  Driven by a simple, readable
YAML file, Zuul has a set of basic concepts that can be combined to
make very powerful automation pipelines.  Zuul can perform speculative
execution of tests on multiple dependent changes in parallel to keep
merges happening quickly for gated projects.

This presentation will illustrate how OpenStack uses project gating as
well as the capabilities of Zuul and how to set up a similar system
for any project.
