---
layout: default
---

There is growing interest in systems that address prospective
information needs against continuous document streams, exemplified by
social media services such as Twitter. Real-Time Summarization (RTS)
is a track at the [Text Retrieval Conference
(TREC)](http://trec.nist.gov) that focuses on these types of
information needs.

## Quick Links

+ The track mailing list [trec-rts@googlegroups.com](https://groups.google.com/forum/#!forum/trec-rts) for participants
+ [Issue tracker](https://github.com/trecrts/trecrts.github.io/issues) for discussions on evaluation design
+ [REST API for Evaluation Broker](https://github.com/trecrts/trecrts-eval/tree/master/trecrts-server)
+ [TREC 2018 RTS Track Guidelines](TREC2018-RTS-guidelines.html)

## What problems are we trying to solve?

We consider users who have a number of "interest profiles"
representing prospective information needs. The system's task is to
automatically monitor the stream of documents to keep the user up to
date on topics of interest. For example, a journalist might be
interested in collisions involving autonomous vehicles and wishes to
receive updates whenever such an event occurs.

We can imagine two methods for disseminating updates:

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

During the official evaluation period, all participating systems
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

## History

Real-Time Summarization (RTS) began at TREC 2016 and represents a
merger of the Microblog (MB) track, which ran from 2010 to 2015, and
the Temporal Summarization (TS) track, which ran from 2013 to 2015.
The creation of RTS is designed to leverage synergies between the two
tracks in exploring prospective information needs over document
streams containing novel and evolving information. The 2016 task
represents an extension of the [real-time filtering
task](https://github.com/lintool/twitter-tools/wiki/TREC-2015-Track-Guidelines)
in the TREC 2015 Microblog Track.

Historic links from previous TREC iterations:

+ [TREC 2018 RTS Track Guidelines](TREC2018-RTS-guidelines.html)
+ [TREC 2018 RTS Final Interest Profiles (Topics)](RTS18_test_profiles.json)
+ [TREC 2017 RTS Track Guidelines](TREC2017-RTS-guidelines.html)
+ [TREC 2017 RTS Initial Interest Profiles (Topics)](TREC2017-RTS-topics1.json): Note that this is the initial set which we are planning to augment based on the interest of the mobile assessors.
+ [TREC 2017 RTS Final Interest Profiles (Topics)](TREC2017-RTS-topics-final.json): Includes interest profiles proposed by both the NIST and the mobile assessors.
+ [TREC 2016 RTS Track Guidelines](TREC2016-RTS-guidelines.html)
+ [Interest profiles that were assessed from TREC 2015](TREC2015-MB-eval-topics.json)
+ [Additional interest profiles culled from TREC 2015](TREC2015-MB-noeval-topics-culled.json)
+ [New interest profiles developed for TREC 2016](TREC2016-RTS-topics.json)
