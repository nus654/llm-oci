Hello. In the previous lessons, we've discussed how large language models compute distributions over vocabulary words and how we can affect those distributions. In this lesson, we'll talk about a few ways we can take these distributions and generate text, otherwise known as decoding.

Let's return to the example we've seen a few times thus far. "I wrote to the zoo to send me a pet. They sent me a--" as we know the LLM produces a distribution over vocabulary words. And the question we're focused on now is, how do we turn this distribution into a word or a sequence of words? Through the course of this discussion, there are a few things that I'd like to drive home. One is that, in decoding, or the process of generating text, it happens one word at a time. It's an iterative process.

Specifically, we give the model some input text. It produces a distribution over words in its vocabulary. We select one. It gets appended to the input, and then we feed the revised input back into the model and perform the process again. In particular, the model is not emitting whole sentences or documents in one step. It all happens one word at a time.

OK, with this in mind, once we compute the distribution over words in the vocabulary, how do we actually pick a word to emit? Well the simplest or most naive, but also effective strategy, we call greedy decoding. And in this strategy, we simply pick the word in the vocabulary with the highest probability. Let's see this method in action.

As we see on this slide, the highest probability word here to fill in the blank is dog. In greedy decoding, we'd select dog, append it to the input, and feed it back to the model. Here, we've done just that. Notice that, when we send the input with dog appended to the end of it back to the model, the probabilities on the remaining words change. In fact, they all get much lower. And we see a new token, EOS, which stands for End Of Sentence, or End Of Sequence, with very high probability.

This is the model telling us, hey, it's very likely that the sentence should end after the word dog. Since we're simulating greedy decoding here, the EOS token is the next word that is selected. After the EOS token, the model is done generating, and the output is returned. Specifically, it's "I wrote to the zoo to send me a pet. They sent me a dog." However, greedy decoding is only the simplest decoding mechanism. In fact, there are many different styles of decoding, some of which are non-deterministic. In other words, they include some random sampling.

In such a regime, you can imagine that, once we have a distribution over vocabulary words, we could take a weighted sample from the distribution, sampling among the high-probability words or even just sampling uniformly. And each of these procedures would produce sentences with different characteristics. Let's take a look at some examples.

Here is another example of decoding. The input is the same as before. And as you might have noticed, I modified the visualized vocabulary words. However, now, instead of picking the highest probability word, we'll pick a word randomly among the visualized choices. Here, we randomly sample the word small. As before, we'll append small to the input and then feed it back to the LLM. As you'll see, the probability on the vocabulary words are revised given this modified input.

In particular, the probability on the word elephant goes down because elephants are typically not small. Again, we'll sample a word randomly from the visualized words. Here, we sample the word red. Finally, you'll notice that the probability on the word panda jumps up because of the existence of an animal known as the red panda. At the same time, the probabilities of the other words go down, since dogs, cats, and alligators are not typically red.

Eventually, the model selects an EOS token or an EOS word and emits the sentence, "I wrote to the zoo to send me a pet. They sent me a small red panda. When decoding with a non-deterministic strategy, that is, when you randomly sample words to emit from the LLM, there's an important parameter to know about, which is called temperature.

What temperature does is it modulates the probability distribution over words. Specifically, when you decrease the temperature, you peak the distribution more around the highest probability word. So for example here, we see that the probability of the word dog has gone up considerably, while the rest of the probabilities have gone down. Again, this simulates decreasing temperature.

On the other hand, when you increase temperature, the probability distribution over words in the vocabulary flattens. That is, all the probabilities get closer together. What you see is that more unlikely words like panther end up having higher probability. One thing that I'd like to emphasize here is that, while the probabilities are being modulated by the temperature parameter, the relative ordering of the words by probability stays the same.

In other words, no matter how we change the temperature, the highest probability word will always have the highest probability. And the lowest probability word will always have the lowest probability. The way that temperature affects the output text is that, when temperature increases and your decoding with a non-deterministic strategy, you're more likely to emit rarer words.

So when temperature is decreased, we get closer and closer to greedy decoding, which we talked about earlier in this lesson. Specifically, this is when we emit the highest probability word at every step. This tends to result in more typical output from the LLM that is generating text. On the other hand, when temperature is increased, the rarer words have a higher chance of being generated. This is typically associated with more creative and even interesting output.

Decoding, whether it with low or high temperature or greedily has its place. When answering factoid questions, you might imagine that we want greedy decoding. That is, we want the most likely words to be generated. On the other hand, if we want the model to generate a story, we want to crank up the temperature and sample some rare words from time to time in order to add intrigue and unpredictability.

Decoding is a fascinating field, and there are entire groups dedicated to studying different methods of generating text so that the text is likely to exhibit specific properties. Before the end of this lesson, I'd like to mention three types of the most common forms of decoding you're likely to encounter. The first is greedy, which we spoke about directly.

The second is called nucleus sampling, which is similar to the sampling-based portion of this lesson but with a few additional parameters that govern precisely what portion of the distribution over words you're allowed to sample from. The last type of decoding, which we didn't talk about, is called beam search where we'll actually generate multiple similar sequences simultaneously and continually prune the sequences with low probability. Beam search is very interesting and helpful because it is decidedly not greedy but ends up outputting sequences that have higher joint probability than the sequences that are output as a result of greedy decoding.

For more information about decoding, there are numerous high-quality resources which should be easy to find online. This concludes our discussion of decoding. Next up, we're going to talk about the phenomenon known as hallucination. 