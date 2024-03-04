---
title: "What Ballot Initiatives Are You Voting For, AI?"
date: 2024-03-03
---

It was just over a week before the 2012 election, and friends were 
gathered at my apartment in Oakland. Amidst dinner and wine, there were careful
discussions about how everyone was planning to vote. California's ballot
 process results in a laundry list of initiatives with innocuous-sounding names
and proposals but whose implications are often inscrutable (with 
[Prop. 13](https://en.wikipedia.org/wiki/1978_California_Proposition_13) a
commonly cited example), and my hope was that a group of motivated friends
might make it easier to figure out what decisions we might make.

In the over ten years since, I have hosted a number of similar parties, both 
for primary and general elections, all with the goal of enabling better
 informed decision making. California, Alameda County, and later San Francisco
County after my move, were all happy to oblige with a number of confusingly 
worded initiatives with unclear implications.

Then there was COVID, which changed the dynamic quite a bit. The 
lack of in person gatherings and people deciding to move to different locations
meant that the number of people participating had slowly dwindled, and my 
motivation to keep hosting the parties started to decline.

That didn't do me any favors when it came time for the upcoming March 5
primary, which has a number of local measures. What has changed in that time 
has been the number of groups that have created voter guides and endorsed
different ballot initiatives. As I looked online, though, I noticed that 
some of my sources, like [SPUR](https://www.spur.org/voter-guide/2024-03), were
only endorsing a subset of initiatives this time and taking no position on
intitiatives like Prop E, which contained a number of sub-proposals and would
 require some research.

As I started my researchn into a spreadsheet, I noticed that I had a number of
other sheets
with endorsement matrices from different organizations in past years (hosting 
parties will do that), along with a lot of free text describing the initiatives
along with pros and cons. Could I use the past endorsements and a language model
to help me predict what my votes might be on these measures?

On a whim, I started putting together a 
[recommender system](https://en.wikipedia.org/wiki/Recommender_system) based on
the data and see how well it would do in predicting endorsements from a held
 out set. Unfortunately, I couldn't find a list of my past votes, so the system
 would create respond with recommendations, where the voter personas would be
for SPUR, [https://www.theleaguesf.org/#propc](The League),
[The Chronicle](https://www.sfchronicle.com/projects/2024/california-primary-election-endorsements/), 
and other sites that have at some point put together voter guides. The features
to the model were based on BERT embeddings of the free text information that I
had collected in those spreadsheets about the ballot initiative.

It took a couple hours to preprocess the data, create train/test splits, 
write a simple
[Factorization Machine](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems)), 
and get my training loss to converge.
indicated that the recommendations being produced were mediocre at best in
generalizing to unseen data, and this held regardless of the number of dimensions
of the underlying latent space. It was at this point that I took a closer look
at the data and discovered my culprit. The text in the spreadsheet was of
 varying quality, and depended on who had been assigned to which ballot measure.
Indeed, changing the level of detail in my eval set would change the outcome of the
 recommendation.

With the election only a few days away, the data cleanup felt a bit too much
 like procrastination on figuring out how I would actually vote. Still, I was
 curious to see how the model would predict SPUR's endorsement of Prop E, the
one on which SPUR had refused to take a position one way or the other. When I
 looked at the outputs on the held
 out set (note that I had held out all of 2024), nearly all of them (with the
 exception of one) assigned either > 0.9 (high probability of a YES endorsement)
or < 0.1 (high probability of a NO endorsement), which meant that the model
was taking a pretty strong position on the opinion of a particular site. Then I
figured out which row and column in my output matrix corresponded to the
SPUR's Prop E prediction, and it turned out to be the exception. For that one,
the model had assigned a probability of 0.4821, almost a fair coin toss.
