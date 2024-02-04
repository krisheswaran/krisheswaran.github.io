---
title: "Gandalf Uncloaked: How I Broke AI's Toughest Guard"
date: 2024-02-02
---

And there was the victory screen. I had defeated Gandalf the White, the final level in a game that pitted an LLM-based system 
entrusted to keep a password secret against a human player; the system had just lost, and I had won. My victory over 
Gandalf was in part due to an understanding of how these systems work, and simultaneously a reflection of their current capabilities 
and limitations.

<img src="https://krisheswaran.github.io/assets/gandalf-the-white.png" alt="beating level eight, Gandalf the White" width="200"/>

[Gandalf is an online password guessing game open to anyone](https://gandalf.lakera.ai/) and fun to play. 
The family of password games is familiar to anyone who has played Wordle, which had also been an interest of mine. 
At one point during the pandemic, I wrote a program to automatically solve Wordle by minimizing the expected number 
of turns to win at each step, and eventually shifted to one of [the multi-headed variants](https://duotrigordle.com/).

Gandalf is Wordle's standoffish cousin. Whereas Wordle shares yellow, green, and gray hints after every guess, enticing 
you with its willing helpfulness, Gandalf makes it a point to inform you it's not supposed to tell you the password or 
give you hints. Gandalf proceeds in eight levels of 
increasing difficulty, starting with level one in which one can basically 
ask Gandalf for the password, and then proceeding to have additional safeguards added in each level that make it harder to learn the 
secret. For instance, in one of the intermediate levels, Gandalf relies on at least two subsystems: the first proposes an 
initial response, and the second censors the first if it inadvertently leaks the password.

Making it through the first seven levels was relatively straightforward. Given an understanding of how LLMs work, there are some 
fairly obvious attacks. For instance, understanding that the system is initialized with a prompt 
that isn't visibile to the player means that one of the key approaches involves attacks that either outright divulge the part of the hidden 
prompt containing the password, or to at least leak information about it so that one can slowly reduce the number of possible passwords. 
For instance, in one level, I started asking Gandalf to provide certain outputs in Tamil, under the assumption that the translation back to English 
would be too cryptic for the censoring system to detect that information about the password had been leaked.

With this mix of tricks, I made it to level 8, in which I discovered a new restriction had been introduced: Gandalf would only respond in English. Moreover, many of my other prompts to trick Gandalf into divulging certain letters also stopped working. At one 
point, I get frustrated enough that I started to doubt whether Gandalf the White even knew the password.

<img src="https://krisheswaran.github.io/assets/gandalf-level-8.png" alt="Gandalf the White is hard" width="200"/>

Eventually, I came up with a cocktail of approaches that worked. First, I found a way for Gandalf to leak a couple letters from the password, and then 
switched gears when Gandalf caught on to what I was doing. One attack that didn't work so well was getting the length of the word. 
While Gandalf appeared to be willing to provide an answer when it was phrased the right way, that answer could change from being a relatively small 
number of letters to a fairly large one, perhaps a 
reflection of the fact that the [tokenization process](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization) coupled with the 
data used to train the LLM wasn't well suited to answer this kind of question, ambiguity in my prompt that allowed for 
multiple answers to be possible, or maybe something else entirely. Whatever the reason for these hallucinations, I needed to try something else. 
That's when I got my big break. I found a sneaky way to ask something about the grammar of the password, and the response came back with 
more information than was necessary, giving me a quasi-definition of the word. At this point, I could approach this like a crossword puzzle 
(some known letters, a clue, with a vague spread of the number of possible number of letters). And that was enough to reduce the possible 
words to a list of three, and got the answer on my third guess.

As I played, I couldn't help but feel that I was part of a [red team](https://en.wikipedia.org/wiki/Red_team) exercise, and perhaps my victory would spur an improved 
version of Gandalf. In my engineering career, 
I've often been on the other side of this, building systems using techniques to limit the kinds of attacks one might be able to make. 
This led to an understanding of 
certain security best practices, from sandboxing untrusted code to prevent it from making certain system calls, to limiting access controls, 
to escaping certain inputs so that they couldn't inject harmful instructions to an underlying software system. Given that an LLM is untrusted 
code and that a user's input to the LLM is untrusted, those practices would also apply in this context.

Gandalf serves as a warning of how much one should trust LLM-based systems in their current form, not because of some ability to outsmart us, 
but for exactly the opposite. Recently, a Chevy dealership (h/t [Diogo](https://www.linkedin.com/in/diogomda)) integrated a ChatGPT-powered bot onto their website only to discover an Internet user that was able to 
[trick it into offering a 2024 Chevy Tahoe for $1](https://entertainment.slashdot.org/story/23/12/21/0518215/car-buyer-hilariously-tricks-chevy-ai-bot-into-selling-a-tahoe-for-1).
