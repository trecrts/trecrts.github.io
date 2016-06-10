---
layout: default
---

Real-Time Summarization (RTS) is a new track at the 2016 [Text
Retrieval Conference (TREC)](http://trec.nist.gov) that represents a
merger of the Microblog (MB) track, which ran from 2010 to 2015,
and the Temporal Summarization (TS) track, which ran from 2013 to 2015.
The creation of RTS is designed to leverage synergies
between the two tracks in exploring prospective information needs over
document streams containing novel and evolving information.  The 2016
task represents an extension of the [real-time filtering
task](https://github.com/lintool/twitter-tools/wiki/TREC-2015-Track-Guidelines)
in the TREC 2015 Microblog Track.

The track mailing list is
[trec-rts@googlegroups.com](https://groups.google.com/forum/#!forum/trec-rts). Please
join if you're interested in participating!

We're using GitHub's [issue
tracker](https://github.com/trecrts/trecrts.github.io/issues) to
discuss details of the evaluation design. Head over there and comment on an
open issue!

## Quick Links

+ [Official TREC 2016 RTS Guidelines](TREC2016-RTS-guidelines.html)
+ [REST API for evaluation broker](https://github.com/trecrts/trecrts-eval/tree/master/trecrts-server)
+ [Guidelines from the TREC 2015 Microblog Track](https://github.com/lintool/twitter-tools/wiki/TREC-2015-Track-Guidelines)
+ [TREC 2015 test topics](TREC2015-MB-testtopics.txt)

## What problems are we trying to solve?

There is emerging interest in systems that automatically monitor
streams of social media posts such as Twitter to keep users up to date
on topics they care about. We might think of these topics as "interest
profiles", specifying the user's prospective information needs. For
example, the user might be interested in poll results for the 2016
U.S. presidential elections and wishes to be notified whenever new
results are published. We can imagine two methods for disseminating
updates:

**Scenario A: Push notifications.** As soon as the system identifies a
relevant post, it is immediately sent to the user's mobile phone via a
push notification. At a high level, push notifications should be
relevant (on topic), timely (provide updates as soon after the actual
event occurrence as possible), and novel (users should not be pushed
multiple notifications that say the same thing).

**Scenario B: Email digest.** Alternatively, a user might want to
receive a daily email digest that summarizes "what happened" that day
with respect to the interest profiles. At a high level, these results
should be relevant and novel; timeliness is not particularly
important, provided that the tweets were all posted on the previous
day.

## General Evaluation Setup

The basic setup of the evaluation is described by the following
figure:

<center><img style="padding-bottom: 15px; padding-top: 5px" src="trecrts-setup.png" width="500px"></center>

The evaluation will occur from August 2, 2016 00:00:00 UTC to August
11, 2016 23:59:59 UTC. During this time, all participating systems
will "listen" to the Twitter sample stream using the Twitter streaming
API and perform the evaluation tasks *in real time*. Systems
will be provided a list of "interest profiles" (similar to topics in
*ad hoc* retrieval) representing users' information needs.

For **scenario A (push notifications)**, content that is identified as
relevant by a system based on the user's interest profile *in
real-time* will be pushed to the TREC RTS evaluation broker (via a
REST API). These notifications will be immediately delivered to the
mobile phones of a group of assessors.

For **scenario B (email digest)**, at the end of the evaluation
period, participants will upload a list of tweets to NIST servers for
evaluation.

For details, refer to the [official TREC 2016 RTS
guidelines](TREC2016-RTS-guidelines.html).
