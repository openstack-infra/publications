Publications Repository
=======================

Each publication should get its own branch and is a living document.
Each branch should have a README.rst file where the first line is the
title of the presentation.

Each time a publication is presented or published, the branch should
be tagged (with a signed, annotated tag).  The first line of the tag
message should be the title of the event or publication, and the tag
itself should be in the format "year-venue-publication".  For example,
if the presentation "overview" was given at LinuxCon North America
2013, you might tag it with:

  git tag -s -m "LinuxCon North America, 2013" 2013-linuxcon_na-overview

The 'make-index' script will create an index page based on index.html,
and all current branches and tags in the repo and their README.rst
files.

Viewable publications are published to:
http://docs.openstack.org/infra/publications
