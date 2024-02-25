---
title: "AI Read the News Differently Now"
date: 2024-02-25
---

The news was hard to bear. I had already deactivated or deleted most of my 
social media accounts, but article headlines and summaries in news feeds, 
even from news sources that I trusted, felt like they were designed to elicit 
the kind of emotional response that would cause me to click through and read 
their content.

So at the start of 2023, I started using OpenAI's _text-davinci-003_ API to 
change how I consumed the news. [NewsAPI.org](https://newsapi.org/) and RSS 
feed libraries provided different mechanisms to access news headlines and 
summaries, so I created a custom news reader to filter how the news initially 
showed up. At the time, my prompt was to just look at the headline:

```
 Summarize the above in one sentence for an important person who wants to get
 the details succinctly, sticking just to the facts and removing opinions.
```

Over time, I evolved the prompt and API, e.g. switching to GPT3.5, and
 experimenting with providing few shot examples. This morning, I took a look
at how my news reader was changing the underlying articles.

<img src="https://krisheswaran.github.io/assets/diff1.png" alt="Ukraine article" width="200"/>

The first focuses on a decade-plus covert relationship between the US and
 Ukraine to mitigate for Russian influence. I was generally satisfied with the
changes made by my reader, in which what initially read like the trailer for a 
movie about a covert op was adjusted into an investigative report on the same 
topic.

<img src="https://krisheswaran.github.io/assets/diff2.png" alt="BBC article" width="200"/>

The second article focuses on an UK politics. As someone who 
hasn't been following this story, it wasn't clear to me whether some of the
 hedging ended up distorting some of the facts (e.g. is "controlled by" a
 better paraphrasing of MP Lee Anderson's statement than "influenced by"?), 
but I did appreciate that the standard gotcha articles in which a politician 
refuses to take a stand on an issue was called out a bit more plainly.

<img src="https://krisheswaran.github.io/assets/diff3.png" alt="Trump-Haley" width="200"/>

The final article is about the Republican primary. I thought this one does
 present a change that distorts content, specifically in how it characterizes
 Haley: "Counterforce within MAGA movement." It might be splitting hairs, but I
 think a more accurate characterization would be a counterforce within the
 Republican Party to the MAGA movement.

While the re-writing of these headlines does sometimes distort the potential 
content of the information contained therein, overall, I have enjoyed the 
more boring presentation of facts compared to the clickbait of the current 
news headlines. This is a news I can bear.
