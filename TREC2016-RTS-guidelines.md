---
layout: default
---

# TREC 2016 Evaluation Guidelines (DRAFT)

## Overview

The TREC 2016 Real-Time Summarization evaluation will take place
from August 2, 2016 00:00:00 UTC to August 11, 2016 23:59:59
UTC. During this time, all participating systems will "listen" to the
Twitter sample stream using the Twitter streaming API and perform the
evaluation tasks *in real time*. The Twitter streaming API offers an
approximately 1% sample of all tweets (sometimes called the
"spritzer") and is freely available to all registered users. Note that
the evaluation time period is in UTC. Track participants are
responsible for translating UTC into their local time to align with
the evaluation start and end times.

During the evaluation period, participants will monitor the Twitter
sample stream with respect to a number of "interest profiles", which
are similar to topics in *ad hoc* retrieval, representing users'
information needs. We use "topic" and "interest profile"
interchangeably.

We consider two scenarios:

**Scenario A (push notifications).** In this scenario, content that is
identified as relevant by a system based on the user's interest
profile *in real-time* will be pushed to the TREC RTS evaluation
broker via a REST API (detailed below). These notifications will be
immediately routed to the mobile phones of a group of human assessors.
The scenario A evaluation setup looks like this:

<center><img style="padding-bottom: 15px; padding-top: 5px" src="trecrts-setup.png" width="500px"></center>

**Scenario B (email digest).** In this scenario, a system will
identify a batch of up to 100 ranked tweets per day, per interest
profile. All tweets from 00:00:00 to 23:59:59 are valid candidates for
a particular day. It is expected that systems will compute the results
in a relatively short amount of time after the day ends (e.g., at most
a few hours), but this constraint will not be enforced. The final
submission (ranked lists of tweets for all days in the evaluation
period) will be uploaded to NIST after the evaluation period ends.

**IMPORTANT NOTE:** During the evaluation period, track participants
*must* maintain a running system that continuously monitors the tweet
sample stream. The track organizers will provide boilerplate code and
reference baselines, but it is the responsibility of each individual
team to run their systems (and coping with crashes, network glitches,
power outages, etc.). A starting point for boilerplate code for
accessing the Twitter sample stream can be found
[here](https://github.com/lintool/twitter-tools/wiki/Sampling-the-public-Twitter-stream).

## Run Types

Each team will be allowed to submit up to three runs for scenario A
and three runs for scenario B. For scenario A, this means that each
team cannot have more than three active client ids with which the REST
API is invoked (during the evaluation period).

Runs for either scenario A or scenario B should be categorized into
three different types based on the amount of human involvement:

+ **Automatic Runs**: In this condition, system development (including
all training, system tuning, etc.) must conclude prior to downloading
the interest profiles from NIST (which were made available before the
evaluation period).  The system must operate without human input
before and during the evaluation period. Note that it is acceptable
for a system to perform processing on the profiles (for example, query
expansion) before the evaluation period, but such processing cannot
involve human input.

+ **Manual Preparation**: In this condition, the system must operate
without human input during the evaluation period, but human
involvement is acceptable before the evaluation period (i.e., after
downloading the interest profile). Examples of manual preparation
include human examination of the interest profiles to add query
expansion terms or manual relevance assessment on a related collection
to train a classifier. However, once the evaluation period begins, no
further human involvement is permissible.

+ **Manual Intervention**: In this condition, there are no limitations
on human involvement before or during the evaluation
period. Crowd-sourcing judgments, human-in-the-loop search, etc. are
all acceptable.

For scenario A, we will ask you for the run type of each run (client
id).  For scenario B, when you are uploading a run, you will be asked
to designate its type. All types of systems are welcomed; in
particular, manual preparation and manual intervention runs will help
us understand human performance in this task and enrich the judgment
pool.

## Interest Profiles

An interest profile is a JSON-formatted structure that contains the
same information as a "traditional" *ad hoc* topic:

```
  { "id" : "MB246",
    "title" : "Greek international debt crisis",
    "description" : "Find information related to the crisis surrounding the Greek debt to international creditors, and the consequences of their possible withdrawal from the European Union.",
    "narrative" : "Given the continuing crisis over the Greek debt to international creditors, such as the International Monetary Fund (IMF), European Central Bank (ECB), and the European Commission, the user is interested in information on how this debt is being handled, including the possible withdrawal of Greece from the euro zone, and the consequences of such a move."
  }
```

The "title" contains a short description of the information need,
similar to what users would type into a search engine. The
"description" and "narrative" are sentence- and paragraph-long
elaborations of the information need, respectively.

The official list of interest profiles is provided using a [REST API
call](https://github.com/trecrts/trecrts-eval/tree/master/trecrts-server)
`GET /topics/:clientid` to the RTS evaluation broker. The API provides
a JSON list of interest profiles in the above schema.

The organizers may add interest profiles during the evaluation period,
in response to emerging events of interest. However, additional
interest profiles will not become "active" (i.e., they will not be
assessed) until the *next* day (in UTC). While this is not totally
realistic, as a user would want to begin tracking an interest profile
immediately, this design simplifies coordination with participant
systems. We will communicate the addition of new interest profiles
over the participant's mailing list, but it is the responsibility of
each system to periodically poll the TREC RTS evaluation broker for
the list of topics. However, please do not poll the API for topics
more than once every hour.

In case there are any inconsistencies, the RTS broker contains the
source of truth for interest profiles.

Note that the RTS broker will return many more interest profiles than
we intend to actually evaluate. The interest profiles that will
actually be evaluated depend on a number of factors, including
assessor interest, available of resources, etc.

## Scenario A Results Submission via the REST API

A system for scenario A must deliver results in real time to the RTS
evaluation broker. This is accomplished via a [REST
API](https://github.com/trecrts/trecrts-eval/tree/master/trecrts-server).
That is, whenever a tweet is identified as relevant to a particular
interest profile, the system must invoke the following call on the evaluation broker:

```
POST /tweet/:topid/:tweetid/:clientid
```

The broker will record the API invocation time as the time the
notification was pushed.

## Scenario B Results Submission via Batch Upload to NIST

Scenario B runs should be formatted as a plain text file, where each
line has the following fields:

```
YYYYMMDD topic_id Q0 tweet_id rank score runtag
```

Basically, this is just the standard TREC format prepended with a date
in format `YYYYMMDD` indicating the date the result was
generated. "Q0" is a verbatim string that is part of legacy TREC
format (i.e., keep it as is). The `rank` field is the rank of the
result, starting with one; `score` is it's score.

This format allows us to easily manipulate the runs and pass onto
existing scoring scripts to compute NDCG, MAP, etc. on a per day
basis. Please make sure that rank and score are consistent, i.e., rank
1 has the highest score, rank 2 has the second highest score,
etc. Otherwise, scoring ties will be broken arbitrarily.

## Evaluation

More details later.


