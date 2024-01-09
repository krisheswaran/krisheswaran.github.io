---
title: "What hallucinations and aliasing have in common"
date: 2023-11-06
---

There was a heat wave in the Bay Area a few weeks ago, and lacking air conditioning, I turned on a ceiling fan. The blades slowly started spinning clockwise, 
but it was a hot day, so I adjusted the fan to the highest setting. As the blades started to speed up, they eventually appeared to shift direction and were 
now spinning counterclockwise. I knew better than to trust my eyes: this was the [wagon wheel effect](https://en.wikipedia.org/wiki/Wagon-wheel_effect), 
an optical illusion that results from temporal **aliasing**. 
Apparently the lights in the room were flickering below the [Nyquist rate](https://en.wikipedia.org/wiki/Nyquist_rate), so like a flip book, each illuminated 
blade was at an angle slightly counterclockwise 
from the previous illuminated blade, and my mind hallucinated the effect.

Hallucination is a word that has taken on additional layers of meaning in the world of large language models (LLMs), and at that moment, I wondered if there was 
a connection between hallucinations in LLMs and aliasing in signal processing. Or were these the idle thoughts of a person succumbing to the heat?

A hallucination occurs when an LLM, given an input sequence of words, generates an output sequence of words that is incorrect, but often appears to be correct to the 
casual observer. This appearance of being correct is in part due to the success of LLMs in producing plausible output sequences for corresponding inputs, but that very 
feature makes the hallucination cases difficult to detect.

To start the analogy, signal processing explores perfect reconstruction of an output given a sampled input. Consider a discrete time signal x[n] for n defined on the 
integers. It is possible to perfectly recover the odd values of x[n] using the even ones (or vice versa) if the following condition holds: X(ω), the [discrete time Fourier 
transform](https://en.wikipedia.org/wiki/Discrete-time_Fourier_transform) of x[n], is bandlimited to π/2 radians, i.e. X(ω) = 0 for π/2 < |ω| < π. The perfect reconstruction 
happens via a sinc interpolation formula, which can be represented 
as a convolution.

We can start to draw a stronger analogy between this sinc interpolation formula and an LLM by adjusting  the problem slightly. Now suppose that x[n] is a wide sense stationary 
random process in which the [power spectral density](https://en.wikipedia.org/wiki/Spectral_density) is bandlimited to π/2 radians. In this case, the same sinc interpolation formula 
turns out to predict the odd values from the 
evens with a mean squared error of zero (it can be shown by proving it is the [Wiener filter](https://en.wikipedia.org/wiki/Wiener_filter)). Note that a mean squared error of zero 
trivially implies [convergence in distribution](https://en.wikipedia.org/wiki/Convergence_of_random_variables), 
so the distribution of the interpolated odd values matches the distribution of the true odd values of x[n], which means that sinc interpolation formula trivially minimizes the cross 
entropy loss. Thus, when the random process is from a distribution that satisfies the constraint on the power spectral density above, the sinc interpolation formula minimizes the cross 
entropy loss of predicting half the values of a sequence when the other half is masked. Given that it can be represented as a convolution, it can be thought of as a linear model (albeit 
one with an infinite number of parameters).

This peculiar framing of a classic signal processing result further draws out the analogy: the LLM is a non-linear model, that via pretraining is designed to predict part of the sequence 
(masked) from another part (unmasked), with the objective to minimize the cross entropy loss when predicting the masked values from the unmasked ones. So we can now see a connection, even 
if tepid, between the LLM and the sinc interpolation formula. What does that have to do with aliasing and hallucinations?

Note that the above results about the sinc interpolation formula all contained an important caveat: the signal needed to satisfy the bandlimited condition. When that condition is not satisfied, 
we then have the phenomenon known as aliasing, in which the sinc interpolation formula will output something that looks plausible but is actually wrong. The fan looks like it’s going in 
reverse. The problem with aliasing is that once the signal has been reduced to its samples, it’s not possible to know that the signal is aliased without additional information, i.e. an 
understanding of how the signal is supposed to look. Thus, it will look plausible to any observer without that additional context. That sounds a lot like what we defined a hallucination to be. 
If hallucinations are at all similar to aliasing, it’s worth noting then that something intrinsic about the context of the signal may have already been lost, making it difficult to recognize 
that a hallucination is taking place.

Before going too deep with this analogy, I was reminded of my senior year in college when I was sitting in [Professor Fine](https://en.wikipedia.org/wiki/Terrence_L._Fine)‘s Feedforward 
Neural Networks class. It was the last semester he 
was offering the course  due to a lack of interest in the subject. On the day in question, Professor Fine was using a Cholesky decomposition to derive the computation of a
[Hessian matrix](https://en.wikipedia.org/wiki/Hessian_matrix). 
A student raised his hand and asked why the professor didn’t just use the Gram-Schmidt process, a trick of linear algebra, to simplify the derivation. The rejection was swift and 
instantaneous: the neural network is non-linear, so the tricks of linear algebra do not hold. I was that student. The lesson stuck. It’s worth noting that there are many places in which 
the analogy breaks down that have been glossed over in this post, not the least of which is that the signal processing results are for a linear system, and LLMs, built on neural networks, 
are non-linear. It will be interesting to see how nuances of the hallucination become better understood over time.
