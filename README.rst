Processing CI Log Events
========================

Abstract
--------

The OpenStack Continuous Integration systems run several thousand tests
during the course of a normal day capturing more than a billion log
events per week. This is a giant treasure trove of information that can
give us CI system performance data, failure frequency, and detect bugs
if the logs are stored in a queryable manner. Using Gearman, Logstash,
and ElasticSearch as building blocks we have built a searchable index of
our test log data. This index provides OpenStack developers with quick
access to why their patches failed to pass tests, trend analysis on
infrequent non deterministic failures, it can flag anomalous log events,
and much much more. Suddenly the mountains of test logs are useful again.

This talk will describe the log processing architecture, what we did to
make it handle over a billion events a week in near real time, and the
neat things we have built around it (including automatic bug house
keeping, trend analysis, and anomaly detection with CRM114).
