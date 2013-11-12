Multi-Master support with the Jenkins Gearman Plugin
====================================================

Abstract
--------

We on Openstack infrastructure team use Jenkins extensively. Our jenkins
servers, at peak load, runs 10,000+ jobs per day.   At that load we require
many jenkins slaves (300+) to process all of those build jobs.  We have
found that our requirement was pushing Jenkins beyond it's limits therefore
we've decided to create the Gearman Plugin to support multiple Jenkins
masters.  The gearman plugin was designed to support extra slaves, allow
load balancing of build jobs, and provide redundancy.  

Jenkins core does not support multiple masters.  You can setup multiple
Jenkins masters but there is no coordination between them.  One problem
with scheduling builds on Jenkins master (“MasterA”) server is that MasterA
only knows about its connected slaves.  If all slaves on MasterA are busy
then MasterA will just put subsequent scheduled jobs on the jenkin server queue.
Now MasterA needs to wait for an available slave to run the jobs.  This is
very in-efficient if your builds take a long time to run.  So.. what if
there is another Jenkins master (“MasterB”) that has free slaves to service
the next scheduled build on the server's queue?  Your probably saying.. “Then
slaves on MasterB should run the jobs instead of waiting for slaves on MasterA
to run them”, then I would say "good thought!".  However MasterB will never
service the builds on MasterA's queue.  The client that schedules the builds
must know about MasterB and then schedule builds on MasterB. This is what we
mean by lack of coordination between masters. This  gearman-plugin attempts
to fill the gap.

This plugin integrates Gearman with Jenkins and will make it so that any Jenkins
slave on any Jenkins master can service a job in the queue.   This plugin will
essentially replace the Jenkins (master) build queue with the Gearman job queue.
The job will stay in the Gearman queue until there is a Jenkins node
(master or slave) that can run that job.  The gearman job queue is shared by
multiple jenkins masters therefore gearman can hand out jobs to the next
available slave on any jenkins master.


References
----------

  Wiki: https://wiki.jenkins-ci.org/display/JENKINS/Gearman+Plugin
  Presentation: http://www.youtube.com/watch?v=pLQddm85fPQ?autoplay=1&rel=1&modestbranding=1&showsearch=0 
