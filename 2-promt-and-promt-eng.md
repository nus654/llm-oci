Welcome back to the OCI learning module on large language models. In the previous lesson, we talked about encoders, decoders, and encoder-decoder models. For the rest of this module, I'm going to be focusing decoder-only architectures because these are the most popular.

And when people talk about LLMs, they tend to be talking about decoder-only models. But I'll also mention that, virtually, all of the content that I will go into applies to encoder-decoders as well. Continuing on, in this lesson, I'll discuss prompting. Let's return to the example we've seen a few times, so far.

I wrote to the zoo to send me a pet. They sent me a-- as we know, an LLM computes a distribution over the next word in the sequence, which I'm illustrating with the probabilities under the visualized words. What I'm going to be covering in this section is how we can exert any control over this distribution, how we can update the probabilities or affect them.

There are two primary ways to do this. The first is prompting, and the second is training. The simplest way to alter the probability of vocabulary words is by prompting. You may have heard the word prompting frequently in Connection to LLMs. Indeed, it's an overloaded term in the sense that it gets used in a lot of different ways.

But the simplest way to think about prompting is that it refers to altering the content or structure of the input that you're passing to the model. This might sound obvious, but when I change the text input to the model, even slightly, I will get a subsequent change in the distribution over vocabulary words.

As an example, imagine that I just appended the word little to the end of the sequence of texts and provided it as input to the LLM. I would get a different distribution over the vocabulary words. In particular, you'll notice that after we append the word little, the probability on the words corresponding to the smaller animals goes up, and the probability on the larger animals goes down.

And conceptually, this makes sense. It's worthwhile to think about how and why the model can do this. Very large decoder-only models are initially trained in a procedure called pre-training. During pre-training, a model is fed a tremendous amount of text that is typically quite varied.

Given a sequence of words, the model is trained to guess at every step what the next word is likely to be and how likely. In some sense, during pre-training, the model should learn, among other things, what little animals exist and, thus, know to make the probabilities of the little animals higher and the big animals smaller.

At a more concrete level, we can hypothesize that the bigram little dog and little cat occur much more frequently in the pre-training text than little lion or little panther. And this accounts for the higher probability on the littler animals. While this is an oversimplification of pre-training, it does give a sense of where these probabilities are coming from.

Now related to crafting model inputs, there is a practice or concept called prompt engineering. This is the process of iteratively refining the model input in an attempt to induce a probability distribution that we like for a particular task. And the way that this is typically done is, literally, by changing the inputs of the model to get closer and closer to the distribution that we want.

Now when you're doing prompt engineering, you wouldn't necessarily be looking at the distribution over vocabulary. Instead, you'd actually be generating text from a model and seeing whether the generated text looks good. Now a couple of important notes about prompt engineering.

First, it can be quite challenging and very unintuitive. If I make a small change in the input text to the model, for example, even adding a whitespace, that can have a large effect on the distribution over vocabulary words. And you don't really know what the change is going to be.

I could rephrase the input. For example, I could say I wanted a pet, so I asked the zoo to send me one. They sent me a-- and this could change the probabilities in ways that I can't predict. So if you spend a lot of time prompt engineering, you may not end up discovering a prompt that works for you.

But at the same time, there have been numerous anecdotal examples that prompt engineering works. So with a very particular task in mind and a very particular model, spending some time trying to come up with the right prompt can be hugely valuable. And there are a number of strategies for doing this that have proved successful in industry and academia.

In the following slides, I'm going to talk about some of these strategies. Here, I'll focus on the most popular, which is the idea of in-context learning. Perhaps, unfortunately, though, the phrase in-context learning does not actually involve learning in the traditional sense. That is with in-context learning, none of the parameters of the model are changing.

Instead, what this refers to is constructing a prompt that has demonstrations of the task that the model is meant to complete. I'll show you an example of this in a second, but I also just want to refine this notion further, with the concept of k-shot prompting, which means including k examples of the task that you want the model to complete in the prompt.

Here is an example from the GPT-3 paper. This came out around 2020, and the goal of this particular prompt is to demonstrate to the model that it should translate English words or phrases into French. And what you'll notice here is that in the prompt, the input to the model literally includes three examples of translation from English to French, followed by a final translation that's incomplete, that we want the model to complete.

This is an example of three-shot prompting. Notice that in the paper itself, they actually labeled different pieces of the input text differently. And this is an example of the term prompt being overloaded. Sometimes, when you hear the word prompt, someone might be referring to the entire input that's being sent to the model.

And that's the way I've been using it through this lesson. But here, to differentiate between the demonstrations or the k-shots, the authors of the GPT-3 paper chose to call their examples the k-shots, the instructions for what the model is meant to do, the task description, and then they define this last piece of the input, the prompt.

Again, I think it's just, technically, the term gets overloaded quite a bit, and it's important to point that out. Finally, I wanted to mention that in the spirit of trying to discuss prompt engineering strategies that work, there are numerous academic and industrial results that show that including these demonstrations in the prompt tend to work better than not including any demonstrations.

By the way, when we don't include any demonstrations in the prompt, it's called zero-shot prompting. In this case, we would have a task description and then jump straight into the task the model is meant to complete. To give you a sense of the variety and design space and prompt engineering, on this slide, I'm going to show a few examples of different prompts.

The first is a two-shot prompt for addition. In it, we show the model two examples of addition and then ask it to add the numbers 1 and 8. Note that the model will not actually perform the computation. Instead, it will generate a probability over words in its vocabulary most likely to follow the expression 1 plus 8 colon.

Second is another very different example that comes from the MPT-Instruct literature. When the MPT-Instruct model is trained, they use the prompt below. It tells the model that, hey, we want you to follow the following instructions, but don't do anything else. Be concise, et cetera.

And then we show the model the instructions it's meant to follow. In this case, I'm asking the model to write a SQL statement for a particular statistic I'm interested in, and then I leave a response field and ask the model to provide the response. Now remember, again, this whole string is being sent as one to the model, and the model is going to generate one word at a time.

That's the way this all works. We pull all the text we want to send to the model together and then have it start generating words one at a time. As a third example, here, we have a very long prompt. You may have seen things like this. I think this prompt gained popularity with the rise of Bing Chat.

Because there was some work and speculation about the length and detail that went into that prompt. And here, just to illustrate this, comes an example from the academic literature. The prompt here has a number of very subtle statements and instructions for the model. It's really detailed.

It includes things like, if you don't an answer, make sure to give this can't response, which is included in the prompt. To summarize, these are just three examples of very different prompts that you could construct. It's meant to give a sense of the vast design space of prompt engineering, but also the versatility of LLMs, and how we can experience this versatility just by changing the input to the model.

As we can see, prompting is quite powerful, and there have been a lot of recent advances and strategies developed towards really interesting styles of prompting. . Here, I'm going to give one example called chain-of-thought prompting. This prompting style came out in 2022 and made the rounds.

In fact, it's still pretty popular and is in wide use today. The idea with train of thought is that if we have a complicated task, here, it's a word problem. In order to solve the word problem, what we're going to do is prompt the model to break down the steps of solving the problem into small chunks, like what you might do if you were solving the problem yourself.

So here, what you'll see the model is doing is stating some of the facts given in the word problem, then reasoning about and explicitly translating some of the information into an equation, writing it out, and solving the equation and giving the answer. This is pretty neat.

And the result in this paper showed that chain-of-thought prompting helps models accomplish some of these harder multi-step tasks than other styles of prompting. I think it's worth it here to pause for a second and think about how this could possibly work.

Because when we give the model this question, remember, it's just generating words one at a time. It doesn't have a high level plan of how it's going to solve this problem. It's literally just generating one word after another. I think that there are two potential hypotheses for why this works.

One is that in the pre-training data, we've actually got examples of problems like this that are broken down into their intermediate steps and solved. And by prompting the model to emit the intermediate steps, the model's actually doing something it learned during pre-training.

The other hypothesis is that when we elicit this kind of problem decomposition, the subproblems that the model generates are manageable in the sense that the model can solve them. If we gave the problem-- if we gave the whole big problem to the model in one go and asked for the answer directly, the model might not get it right.

But if we ask for the problem to be broken down into small chunks, the problem becomes more manageable. I think this is a really interesting-- this is a really interesting phenomenon, because it almost mimics the way that a human might solve this problem.

I wouldn't necessarily call this reasoning, but it imitates reasoning in a nice and convincing way. So on the topic of problem decomposition, there's been another piece of work that we can refer to as least to most prompting. Here, we ask the model to solve simpler problems first and use the solutions to the simple problems to solve more difficult problems.

In this task, what the model is supposed to do is, given a list of words, concatenate the last letter of each of those words together. You can imagine that this gets harder and harder as the list of words gets longer. But what the researchers did is taught the model to solve these problems in increasing order of difficulty.

So for example, the model should start with the first word, get its last letter, and then it should look for the first two words, and concatenate the last letter of-- the last letter of the second word, with the solution to the first subproblem. I'll point out here that the model is doing precisely that.

So here, it's saying, hey, I think I've solved think machine, and it knows that the output think machine is ke. And the last two letters-- the last two letters, ke, are all that it needs. What it does here is it looks at the last word, learning, and says, hey, I've solved think machine before, and I know that the output is key.

So I'll just emit the last letter of learning, which is G, with the solution to think machine, which is ke, and it gets the word right. Perhaps, unsurprisingly, this works better than chain-of-thought prompting and other prompting strategies. The last style of prompting that I'll bring up comes from DeepMind, where they taught the model to improve its performance on chemistry and physics questions by reasoning about the concept or explicitly mentioning the concepts that are required to solve the equations presented.

And what they found was that when you ask a model to a complicated question from physics or chemistry, but have it first emit the first principles and equations required to solve these problems, the model has a much higher success rate. In this lesson, we talked a lot about how we can have a model accomplish a variety of tasks, just via prompt engineering. In the next lesson, we'll take a look at how prompt engineering can also be employed to elicit bad behavior from a model. Stay tuned. 
