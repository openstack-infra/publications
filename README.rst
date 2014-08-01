Template Branch for new OpenStack Infra Publications
====================================================

Creating new OpenStack Infra Publications is easy and you have started
in the right place.

  1. Clone publications, create and checkout template tracking branch::

       git clone git://git.openstack.org/openstack-infra/publications
       cd publications
       git review -s
       git checkout -b template origin/template

  2. Create a new branch based on this template branch.
     ``git checkout -b $BRANCH_NAME``.
  3. Edit ``.gitreview`` and change the defaultbranch value to
     ``$BRANCH_NAME``.
  4. Create ``$BRANCH_NAME`` in Gerrit. It should be based on the
     template branch as well to avoid any potential merge conflicts in
     your first commit. Not everyone has the ability to do this in
     Gerrit. If you don't, ask an openstack infra core to do it for you.
  5. Now we get to do the fun stuff. Edit index.html editing lines with
     ``CHANGEME`` or ``changeme`` in them. You can also add new slides
     if you like but that isn't necessary in this bootstrapping change.
     You can follow up with new slides in subsequent changes.
  6. Edit this file, ``README.rst``. The title of this document will
     be the name used on the root publications index so be sure to
     update the title. You should also add an Abstract section and
     general talk info.
  7. At this point you are ready to push your new changes back up to
     Gerrit. ``git commit -a && git review``
