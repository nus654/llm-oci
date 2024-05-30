Welcome back to the OCI learning module on large language models. In the previous two lessons, we talked about prompting as a way to affect the model's distribution over vocabulary words. But prompting is not the only option for affecting this distribution. In fact, a more significant way to alter the distribution over vocabulary is training, which we'll talk about in this lesson.

Remember that prompting is, in effect, simply changing the input to an LLM. The process is highly sensitive. In other words, small changes in the prompt can yield large changes in the distribution over words. Moreover, since the model's parameters are fixed, by using prompting alone, we're limited in the extent to which we can change the model's distribution over words.

In this way, sometimes, prompting is insufficient. For example, in domain adaptation, that is when a model is trained on data from one domain, and then you want to use it in an entirely new domain, you might need something more dramatic. As opposed to prompting, during training, we're actually going to change the parameters of the model.

I won't go into detail on what happens during training. But at a high level, you can think of training as the process of giving the model an input, having a guess a corresponding output, for example, the completion of a sentence or an answer to an input question, and then, based on this answer, altering the parameters of the model so that next time, it generates something closer to the correct answer.

As may be clear, once you alter the parameters of the model, the distribution over words that the model computes on any input changes and, hopefully, for the better. There are many ways that you can train or, in other words, change the underlying parameters of the model. Four such approaches are shown in this chart, and they all come with their own advantages and costs.

In the first row here is fine-tuning, which is around 2019, the way that we trained all language models. In fine-tuning, we take a pre-trained model, for example, BERT, and a labeled dataset for a task that we care about and train the model to perform the task by altering all of its parameters.

Training a BERT model was, at the time, thought to be somewhat expensive. But it's nowhere near as expensive as training the models of today, which are orders of magnitude larger. Because full fine-tuning is so expensive, we've turned to cheaper alternatives, like the family of parameter efficient fine-tuning methods.

In these methods, we isolate a very small set of the model's parameters to train, or we add a handful of new parameters to the model. One of the methods you might have heard of in this space is LORA, which stands for Low Rank Adaptation. In this method, we keep the parameters of the model fixed and add additional parameters that will be trained.

Soft prompting is another cheap training option. Although, the concept here is different than methods like LORA. In soft prompting, what we're going to do is actually add parameters to the prompt, which you can think about as adding very specialized, quote, unquote, "words" that will input to the model in order to queue it to perform specific tasks.

Unlike prompting, a soft prompt is learned. Or in other words, the parameters that represent those specialized words we added to the prompt are initialized randomly and iteratively fine-tuned during training. The last training I want to bring up is continual pretraining, which is similar to fine-tuning in that it changes all the parameters of the model.

So it's expensive, but it's different in that it does not require a label data. Instead of training a model to predict specific labels, during continual pre-training, we just feed in any kind of data that we have for any task that we have and ask the model to continually predict the next word.

If we're trying to adapt a model to a new domain, let's say, from general text to a specialized domain of science, continually pre-training or simply training the model to predict the next word in millions of sentences from that specialized scientific domain can be pretty effective.

I want to say a bit more about the cost of training. And to help, I've provided this chart. My colleagues and I have tried to estimate the cost of some of these training approaches for various-sized models. Now I have to caveat this significantly and say that there are a lot of factors that would affect these numbers.

For example, how long do you want to train for, how much data do you have to train on, what kind of GPUs do you have, how many, et cetera. The numbers in this chart come from training that we've performed on our own hardware or have been presented in recent research papers.

What you should notice here is the scale of what's required. For example, all the way on the right of the chart, you can see the costs of generating text from an LLM. These costs are relatively cheap. With a 7-billion parameter model, you can get away with generating text on a single GPU, usually in a few seconds.

With a large model, say more than $150 billion parameters, you might need as many as 8 or even 16 GPUs to generate text, depending on the precision of the model. Going to the left in the chart, to the parameter efficient methods, you see that training, even a small number of parameters requires a handful of GPUs for a few hours.

All the way to the left of the chart, we have some estimates for the cost of pre-training. Notice that this takes hundreds or even thousands of GPUs for many days. This is extremely expensive. Finally, I just want to point to one paper here, which looks at training from a different angle.

The paper presents what they call cramming and studies the question, how far can you get if you have a single GPU and 24 hours to train a model? If you're interested in that, this is a really nice read that I'd encourage you to take a look at. With that, we've wrapped up our discussion of training. And in the next lesson, we'll talk about decoding. 
