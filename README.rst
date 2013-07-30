Abstract
========

Scaling OpenStack Development: Continuous Integration Overview
--------------------------------------------------------------

OpenStack is not only the fastest-growing open-source cloud project but
is also a large-scale, complex system with a rapidly expanding code base
and more than 1,000 contributors to date.  Handling the quantity and
pace of contributions is a huge challenge on its own.  We've been able
to handle the dramatic scale of development by having automation systems
that allow us to treat all developers equally from a process perspective
and keep our trunk always clean by performing testing pre-merge.  The
beautiful thing about this approach has been that it doesn't just keep
up with demands, it facilities and encourages more development.

This talk will cover the design and implementation of the current
system, based around a combination of Gerrit and Jenkins, as well as the
workflow that we support and require, how we implemented it and what the
challenges were.  At the end of this talk you should have a good
understanding of how OpenStack handles up to 200 contribution
activities an hour.

Talking points
==============

The OpenStack Grizzly release brought roughly 400,000 new lines of
source code in 10,000 changes from 500 developers over a 6-month period.
Every change passed a battery of style, unit, functional and integration
tests over the course if its development and review, and again before
being merged into the official codebase. This presentation will provide
a high-level examination of the techniques used to coordinate and
automate software development efforts at such a scale.

    * Projects:
        - scaling challenge faced as a community
        - number of individual software projects being integrated
        - server projects are part of an integrated release
        - client library projects are released on separate schedules
        - incubated projects shown in gray
    * Programs/Horizontal Efforts:
        - scaling challenge faced as a community
        - many important contributions are not focused on a project
        - might span multiple software projects
        - could be something other than traditional software development
    * Release Management:
        - scaling challenge faced as a community
        - integrated release and roadmap follow a rigid schedule
        - limitations chosen to improve output and quality
    * Contributors:
        - scaling challenge faced as a community
        - contributors come from varied places and backgrounds
        - different levels of involvement
        - have a variety of goals and motives (usually not a bad thing)
        - there are many, many, many of them
    * Consistent Tooling:
        - meta-development happens independently without consistency
        - consistency increases throughput with fewer people
    * Developer Infrastructure:
        - both a scaling challenge and solution
        - vast array of systems used for development efforts
    * Developer Environment
        - operating systems and python versions supported (and how that
          impacts testing)
        - developers on IRC aids distributed development
        - openstack is complicated to install; devstack makes it simple
        - lots of testing helps stabilize rapid development and
          facilitates contributions
    * Project Gating
    * Everything Is Automated
    * Process Flow
    * Gerrit
    * Gerrit (screenshot)
        - change information
        - commit message
        - bug and blueprint linkage
        - review status, categories
        - patchsets
        - comments
        - pre merge testing
        - gating
    * Gerrit Diff View
    * Bug Integration - Launchpad
    * Approved Reviews
    * Git Review
    * Types of Tests
    * Specific Challenges/Solutions
    * Gerrit Git Prep
    * Interrelated Integration Testing
    * Devstack-Gate Problems
    * Devstack-Gate Solutions
    * Zuul
    * Bottlenecking
    * Zuul Simulation:
        1. branch tip of repositories for nova and keystone
        2. changes enter the gate pipeline, merged to a test queue
        3. zuul initiates tests on each in parallel, keystone fails
        4. first change passes all tests
        5. merged to nova and becomes the branch tip
        6. second change passes all tests
        7. merged to nova and becomes the branch tip
        8. third change is ejected and keystone branch tip is unchanged
        9. fourth change is merged to a new test queue, now in first
        10. zuul restarts tests on the new queue of one change
        11. first change passes all tests
        12. merged to nova and becomes the branch tip
    * Zuul Check Pipeline
    * Zuul Gate Pipeline
    * Zuul Post-Merge Pipeline
    * Zuul Release Pipeline
    * Zuul Project Configuration
    * Templated Jobs
    * Example Job
    * Example Template
    * Scaling Hardware Needs
    * Thanks!
