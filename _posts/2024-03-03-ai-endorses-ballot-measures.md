---
title: "What Ballot Initiatives Should I Vote For, AI?"
date: 2024-03-03
---

It was just over a week before the 2012 election, and friends were 
gathered at my apartment in Oakland. Amidst dinner and wine, there were careful
discussions about how everyone was planning to vote. California's ballot
 process results in a laundry list of initiatives with innocuous-sounding names
and proposals but whose implications are often inscrutable (with 
[Prop. 13](https://en.wikipedia.org/wiki/1978_California_Proposition_13) a
commonly cited example), and my hope was that a group of motivated friends
would make it easier to figure out how to cast informed votes.

In the over ten years since, I have hosted a number of similar parties, both 
for primary and general elections, all with the goal of enabling more
 informed decision making. As for the motivation for these parties,
the state of California, Alameda County (and San Francisco
County post-move), were more than happy to oblige with a number of confusingly 
worded initiatives with unclear implications.

Then came COVID, which completely changed the dynamic. The 
lack of in-person gatherings combined with friends moving away
meant that attendance slowly dwindled along with my motivation to keep hosting.

That didn't do me any favors when it came time for the upcoming March 5
primary, which as usual has several local measures. What has changed since
my first ballot party is that there are a number of web sites offering
voter guides, mostly created by different special interest groups. As I looked
 online, though, I noticed that 
some of my sources, like [SPUR](https://www.spur.org/voter-guide/2024-03), were
only endorsing a subset of initiatives this time. While I don't always agree 
with SPUR, I've found their analysis on the pros and cons of different ballot
measures helpful, and it looked like they weren't providing this for the 
measures they weren't endorsing. This included Prop E, which contains a number
of sub-proposals and would require some research.

As I compiled that research into a spreadsheet, I noticed 
other sheets in my drive from earlier ballot parties. These sheets
included endorsement matrices from organizations like SPUR, along
 with free text descriptions of the initiatives, as well as their
pros and cons. Could I use the past endorsements and a language model
to help me predict what my votes might be on these measures?

On a whim, I started putting together a 
[recommender system](https://en.wikipedia.org/wiki/Recommender_system) based on
the data and see how well it would do in predicting endorsements from a held
 out set. Unfortunately, I couldn't find a list of my past votes, so the system
 would respond with recommendations treating each web site as a 
voter persona, so I could browse the recommendations 
for SPUR, the [League](https://www.theleaguesf.org/#propc), the
[Chronicle](https://www.sfchronicle.com/projects/2024/california-primary-election-endorsements/), 
and other sites that had put together voter guides in past years. I decided to use 
[BERT](https://en.wikipedia.org/wiki/BERT_(language_model)) as my language model
 to convert the ballot-related text into embeddings.

The process was surprisingly straightforward. Within a couple hours, 
I had preprocessed the data, created train/test splits, 
written a simple
[Factorization Machine](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems)), 
got my training loss to converge, and done a basic hyperparamter sweep. That's 
where the good news ended. My evals
indicated that the recommendations being produced were mediocre at best.
It was at this point that I took a closer look
at the data and discovered one possible culprit. The text in the sheet was of
 varying quality, which in turn depended on who had been assigned to which
 ballot measure. Indeed, subtle changes to the text changed the outcome of the
 recommendation. Furthermore, despite years of ballot parties, we weren't
 talking about a lot of data, so it wasn't surprising to me that the model
 would overfit.

While I had some ideas on how to address these challenges, with the election only
 a few days away, implementing them felt 
 like procrastinating on the actual task of how I would vote. Still, I was
 curious to see how the model had predicted SPUR's endorsement of Prop E, the
one on which SPUR had refused to take a position one way or the other. When I
 looked at the model's predictions on 2024 ballot initiatives (I had held out all of 2024), the model had assigned 
nearly all of them a probability > 0.9 (likely YES endorsement)
or < 0.1 (likely NO endorsement). Despite the noted problems with the model
itself, I was nonetheless quite excited to see how it had placed its bet on
 SPUR and Prop E. I cross-referenced the correct row and column corresponding
to SPUR's Prop E prediction and realized then that it was the one exception for 
which the model had not assigned a high or low probability. Instead,
the model had assigned a probability of 0.4821, refusing to take a position one
way or the other. 

After my efforts, I sought out a zero-shot opinion on the
 matter via ChatGPT because why not? It provided a few paragraphs of analysis followed by
the following statement: "As of now, there hasn't been a specific recommendation
 from SPUR (San Francisco Bay Area Planning and Urban Research Association) or a
 direct statement on their stance regarding Proposition E." I returned to my ballot research.
