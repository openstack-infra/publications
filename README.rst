Code Review for Systems Administrators
======================================

The OpenStack project uses a public code review system and automated series of
unit and integration tests before merging to confirm that code submitted is
adhering to project standards and doesn't cause problems for other software in
the stack.

The OpenStack Infrastructure team not only manages this system using open
source tools like Gerrit and Jenkins for review and testing, but also uses the
system themselves for reviewing and testing changes being made to systems
running the infrastructure for the project. Puppet configuration files, Python
scripts and more are subjected to automated syntax tests and then
collaboratively reviewed in public by community and core team members alike
before approval.

This process has allowed the team to have a considerably open approach to
systems administration within the project infrastructure. It has also made it
much easier to work on effective solutions through code and configuration
sharing during the review process. With recent improvements to documentation it
has allowed also for easier on-boarding of new and casual contributors looking
to get involved with assisting with infrastructure work.
