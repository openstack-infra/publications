Consuming Open Source Infrastructure
====================================


Infrastructure and configuration are now being represented as code. This code
is then put into git repositories, OSI approved licenses are attached, and the
code published. This creates an open source project. There are several instances
of this now: OpenStack, Mozilla, Wikimedia, and Jenkins all have open sourced
their infrastructure. It is, however, relatively easy to say "our configuration
is totally open source, anyone can use it", and it is actually much harder to
actively consume someone else's configuration. My team consumes one of these ope
n source configuration projects and sits downstream from it. I will present on
what we're doing, what has worked, what hasn't, and what we're going to do next.
I'm going to give actionable advice for people who are consuming or want to be
cons uming another organization's open source infrastructure, and I'll be
providing some feedback to those who are currently open sourcing their
infrastructure on how to make it easier to consume.


OpenStack's infrastructure team has an open source infrastructure primarily
using the Puppet configuration management tool. Using hiera they are able to
separate secrets from Puppet code, and using roles they can keep OpenStack
specific logic from generically reusable configuration. The infrastructure is
multifaceted but the core of it is Gerrit for code review, cgit for code
browsing, zuul for merging/gating, Jenkins and gearman for testing with apach,
mysql, and zmq doing what they do best.


My team at HP consumes this open source infrastructure and replicates it
internally. We use their Puppet code, and do the dance of the downstream:
patch/submit patch upstream/reconsume patch after it has landed upstream. We
call the project Gozer and our admins are called Ghostbusters. We attend the
weekly meeting that upstream holds, and some of us are well on our way to
having our upstream commit bits, but our core focus is on maintaining the
downstream ci/cd pipeline for HP. Configuration management is the reason any
of this is possible. I'm going to talk about specific ways Puppet code can be
written to be re-consumable, and highlight a couple 'dead ends' we walked
down before finding some successful patterns.


This presentation covers:


* The problems upstream is solving, the problems downstream is solving, where
those goals align and where they differ

* How we bootstrapped our infrastructure (and why that was a
problem)

* How we participate upstream

* How the Puppet codebase has evolved to be more consumable, where it started,
and where it is now

* How we dealt with different network topology between our infrastructure and
upstream's infrastructure

* How we maintain parity with upstream (consistently consuming it)
