---
title: "AI Chatbots As My Coding Best Frenemy"
date: 2024-02-22
---

The code was a total mess. I'd written it at some point in 2022 to help me solve
Wordle and its many variants. The new goal was to refactor the code to make 
it easier to accommodate a new frontend interface. However, I couldn't
 decipher the logic of much of what I had written, beyond the sparse commenting
 or the logic behind different parts beyond the sparse commenting 
that I had written up a couple years ago.

If this had been a work project, it would have been different. After some 
period of hacking / exploration, I would prepare my code for review, optimizing 
for future debugging in its design and comments, as well as providing a robust 
suite of unit tests. At least one person would review the code to help me
identify places in which the design might benefit from changes. Along the 
way, a range of devtools and
 [style guides](https://google.github.io/styleguide/) have made it a lot 
easier to follow best practices.

When it comes to personal projects, I am not so disciplined. That
makes it hard to continue things or invest in things, and code rot combined
with lost motivation usually dooms these efforts.

Yet there it was, a mix of functions with names like _find_num_turns(...)_ and
_find_num_turns_variant(...)_ that I was struggling to decipher. So I went to 
an AI chatbot, typed in my code along with the following prompt:

```
Help me comment this code in a way that follows the Google Python style guide
```

The output effectively refactored my code along with comments that helped me
understand exactly what I had done, along with why I had done it. As I went 
through the comments, I found myself understanding the code. An LLM-based
chatbot had made my code more readable to me. Then for an encore, I decided to
 follow it up by providing my unit tests with this prompt:

```
That's my unit test. Could you bulk it up to create a more comprehensive test of my code
```

What resulted was a comprehensive set of unit tests. I looked at everything
that had just taken place, realizing that what might have been the product of 
a day or two at work, including a back and forth with code reviewers, had just 
been handed to me via a couple of prompts. I called Aarti into the room,
 showed her what had happened, and introduced her to my new friend.

So I copied the code back into my workspace and ran the tests. They FAILED. Ugh.
I also noticed that within my workspace, the code didn't strictly adhere to 
parts of the style guide like the 80 character line limit, causing me to resize
some of my terminal windows (did I mention that Vim is my go to IDE sometimes?).

As I looked at the tests, I found a frustration that I've long had with LLMs,
and the false sense of security they seem to provide because they do so many
things so well. Specifically, when it came to some of the positional assertions
in Wordle, the tests were entirely wrong about where the green, gray, and
 yellow tiles should appear. While I can't be certain, my guess is that it's 
for the same reason that the 80 character line limit was also a challenge:
tokenization.

Tokenization is the process in which text is split up into smaller units called
tokens that can be fed into the language model. The language model only works on
these tokens, numerical representations of the underlying text. Tokens can
 consist of multiple characters but don't necessarily fall at word boundaries or
 have a fixed length. Because all this is abstracted away for the language
 model, its ability to address certain kinds of questions related to the
 position and ordering of letters, words, etc. will depend both on the
 tokenization algorithm used as well as the training data. My hunch was that I
was encountering a problem related to this.

So I went in and thought through each test case, and within about an hour, had 
fixed everything so that the tests were passing. Also, tools like _pylint_ made
it easier to fix some of the smaller errors that my AI assistant had made with
 the formatting. In total, I had saved time on coding, but some of the magic 
and my trust in the LLM were diminished. Aarti saw my face, and asked how
 things were going with my new friend. Frenemy, I responded.

Incidentally, as I was finishing up the code,
 [Andrej Karpathy](https://en.wikipedia.org/wiki/Andrej_Karpathy) had just
 posted a
 [video about tokenization](https://www.youtube.com/watch?v=zduSFxRajkE),
 and my experience was the perfect motivation to 
watch it.
