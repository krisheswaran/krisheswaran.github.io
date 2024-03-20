---
title: "Your City in Numbers"
date: 2024-03-17
---

We're in our kitchen with a couple of IPython notebooks open. Aarti has used
SQL before, but with the help of an LLM is able to query the troves of city
data that are contained inside the 
[pandas dataframe](https://en.wikipedia.org/wiki/Pandas_(software)). It is
one of many datasets that the city provides through its
[open data initiative](https://datasf.org/opendata/), and it turns out there
is [a standard](https://dev.socrata.com/) that multiple cities
 (including NYC, LA, and Seattle) use to provide the 
public access to everything from 311 cases, crime, government contracting,
 transporation, and lobbyist firms registering with the City's Ethics
Commission.

<img src="https://krisheswaran.github.io/assets/san-francisco.jpg"
     alt="from a recent flight over San Francisco in August of 2023"
     width="200"/>

Our goal is to try to understand ways to help the city work more effectively,
and which actions might have the most impact. Sifting through the data gives
 us an understanding of things like San Francisco's procurement process and
also a sense of frustration at being provided with so much data, but ultimately
despite a number of open standards, how difficult it actually is to work with.

Data has certainly been key in driving a variety of decisions in my day job,
and perhaps the most important is which problems and areas to focus on. The 
hope is that we can do something similar in engaging locally. I write some 
convenience functions to better analyze the data. I feel a tap on my shoulder. 
Aarti points me to a graph she's created. I smile. 
