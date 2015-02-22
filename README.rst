Scaling Your Jenkins Jobs
=========================

The OpenStack project is developed by one of the largest open-source
communities in the world. There are currently over 1000 active
contributors world wide producing 1,500 changes per day across more
than 300 git projects. It is a very active project and is growing
very quickly.

The OpenStack continuous integration infrastructure relies heavily on
Jenkins.  Our system has grown to require over 4,000 Jenkins jobs
to run all of the builds and tests across all of the OpenStack projects.
Supporting that many jobs can be quite insane so we created the Jenkins
Job Builder (JJB) to help us automate and manage that complexity. JJB is
an open source application that takes simple descriptions of Jenkins
jobs in YAML format and uses them to create and configure Jenkins
projects. JJB is written in Python and has a powerful template engine
that allows us to easily create many Jenkins projects with similar
configurations.  We are using JJB to create new jobs and update
existing jobs across multiple build and test dimensions.  We’ve
integrated JJB with a code review tool (Gerrit) to allow our developers
to review every job that is created and updated in our CI system.
We’ve also integrated JJB with a configuration management tool (Puppet)
to automate the execution of JJB on every change to our Jenkins jobs.
Since we’ve enabled multiple Jenkins masters, JJB is now used to
automate and manage over 30,000 Jenkins job!

This talk is to discuss how we designed Jenkins Job Builder, how it helped
us scale out the OpenStack CI infrastructure and how it can be used in your
CI system as well.
