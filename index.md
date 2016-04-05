---
layout: default
---

Real-Time Summarization (RTS) is a new track at the 2016 [Text
Retrieval Conference (TREC)](http://trec.nist.gov) that represents a
merger of the Microblog (MB) track, which has been running since 2010,
and the Temporal Summarization (TS) track, which has been running
since 2013. The creation of RTS is designed to leverage synergies
between the two tracks in exploring prospective information needs over
document streams containing novel and evolving information.  The 2016
task represents an extension of the [real-time filtering
task](https://github.com/lintool/twitter-tools/wiki/TREC-2015-Track-Guidelines)
in the TREC 2015 Microblog Track.

## What problems are we trying to solve?

**Scenario A: Push notifications to mobile phones.** Let us assume a
stream of social media posts such as Twitter, against which the user
issues an arbitrary number of standing queries representing "interest
profiles", analogous to topics in ad hoc retrieval. For example, the
user might be interested in poll results for the 2016
U.S. presidential elections and wishes to be notified whenever new
results are published. The system's task is to identify interesting
tweets from the stream and send these updates directly to the user's
mobile phone via a push notification. At a high level, push
notifications should be relevant, timely (provide updates as soon
after the actual event occurrence as possible), and novel (users
should not be pushed multiple notifications that say the same thing).

**Scenario B: Periodic email digest.** Building on the above scenario,
a user might want to receive a periodic (e.g., daily) email digest
that contains interesting tweets with respect to the interest
profiles. At a high level, these results should be relevant and novel;
timeliness is not particularly important, provided that the tweets
were all posted on the previous day.


## General Evaluation Setup

The basic setup of the evaluation is described by the following
figure:

<center><img style="padding-bottom: 15px; padding-top: 5px" src="trecrts-setup.png" width="500px"></center>

The evaluation will occur during a specific period of time in August
2016: During that time, all participating systems will "listen" to the
Twitter sample stream using the Twitter streaming API and perform the
tasks (detailed below) *in real time*. Prior to the evaluation period,
systems will be provided a list of "interest profiles" (similar to
topics in *ad hoc* retrieval) representing users' information
needs. We consider two evaluation scenarios:

**Scenario A: Push notifications on a mobile phone.** Content that is
identified as interesting by a system based on the user's interest
profile *in real-time* will be pushed to the TREC RTS evaluation
broker (via a REST API). Putatively, these notifications are delivered
to users' mobile phones.

**Scenario B: Periodic email digest.** On a daily basis, the system
aggregates the most interesting tweets with respect to each interest
profile and pushes the results to the TREC RTS evaluation broker (via
a REST API). Putatively, these results are sent to users in the form
of email digests.

The TREC RTS evaluation broker will pass system results to a pool of
assessors, the details of which have yet to be worked out.

