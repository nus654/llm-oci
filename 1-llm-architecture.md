Hello, and welcome to lesson 2 of this OCI learning module on large language models. In this lesson, we'll talk about LLM architectures. I will be focusing on two major architectures for language models. The first is encoders, and the second, decoders. These architectures largely correspond to two different tasks or model capabilities that you may have heard of.

The first capability is embedding and the second is text generation. And before I get into them, I'll mention that both encoders and decoders are built atop a building block called a transformer. OK, when we say we're embedding text, we're generally referring to the process of converting a sequence of words into a single vector or a sequence of vectors.

In other words, an embedding of text is a numeric representation of the text that typically tries to capture the semantics or meaning of the text. The process of text generation is pretty self-explanatory. The input to a text generation model is a sequence of words, and the output is a generated sequence of words.

Encoder models are designed to encode text, that is produce embeddings, and decoder models are designed to decode or generate text. All the models that I'll be talking about in this module are based on an underlying transformer architecture, which was popularized in the paper, Attention Is All You Need, which came out in 2017.

That paper has really revolutionized natural language processing and machine learning at large. I'm not going to talk about the transformer architecture in detail, but there are a number of good tutorials out there, which I'd encourage you to take a look at if you're interested. Encoders and decoders can come in all different kinds of sizes.

In the realm of language models, size refers to the number of trainable parameters that the model has. To give you a sense of how big that is the number of trainable parameters some of the models are, I've created this model taxonomy, broken down into three different buckets corresponding to architecture-- encoders, decoders, and a combination model called an encoder-decoder.

I've deliberately tried to include models that are discussed in the mainstream media or are ubiquitous in research papers. There are two main items to take away from this chart. The first is to pay attention to the fact that the y-axis of the chart does not increase linearly but rather by orders of magnitude.

That is, as we go up, each dotted line represents a factor of 10 increase from the previous dotted line. The second thing to notice is that the decoder models tend to be pretty large, especially compared to the relatively smaller encoders. The reason for this is largely historical.

There's no reason why we couldn't make a really large encoder, but previous work has shown that we don't really need to. On the other hand, when models are too small, they tend to be poor text generators. However, recent research has shown glimmers of this pattern changing.

That is with a bit of added cleverness, we may be able to generate fluent text with small models. Let's talk about encoders in more detail. Encoders are designed to embed text, and as I mentioned before, that means taking a sequence of words and converting it to vectors.

Here, I'm showing an illustration of how that happens in a BERT-style model. We provide the model the text, "They sent me a," which you might remember from the first lesson in this module. And what the model produces is a vector representation of each word that was passed through, in addition to a vector representation for the entire sentence.

Now these vector representations are designed to be consumed later by other models to do things like classification or regression. But there are a lot of-- but a lot of their use nowadays has also been for vector search in databases or so-called semantic search. That is, let's say you want to take an input text snippet and retrieve a similar document from a corpus.

To accomplish this, you could encode or synonymously embed each document in the corpus and store them in an index. When you get the input snippet, you encode that, too, and check the similarity of the encoded input against the similarity of each document in the corpus. And then you return the most similar.

Now apart from encoders, we have decoder models. Some decoders you may have heard of are the Cohere command model, GPT-4 or Llama. What these models do is they take a sequence of tokens and emit the next token in the sequence, based on the probability of the vocabulary which they compute and which we discussed in the first lesson.

Importantly, a decoder only produces a single token at a time. This is very important to remember. We can always invoke a decoder over and over to generate as many new tokens as we want. In more detail, to generate a sequence of new tokens with a decoder, what we need to do is, first, feed in a sequence of tokens and invoke the model to produce the next token.

Then append the generated token to the input sequence and feed it back to the model so that it can produce the second token. But given the size of these models, this is computationally very expensive. Note that, typically, you would not use a decoder model for embedding. Instead, you'd use an encoder.

Decoders are really in vogue now because they've shown tremendous capability for generating fluent text. Moreover, they've been shown capable of doing things like answering questions, participating dialogue, and more. The final architecture that I'll briefly mention are encoder-decoder models.

These are constructed exactly as they sound. You kind of glue a decoder onto an encoder. Encoder-decoder models have primarily been utilized for sequence-to-sequence tasks like translation. What I'm showing here is an example of translation with an encoder-decoder model.

The way that this works is as follows. We send the English tokens to the model. They get passed to the encoder, which will embed all the tokens in addition to the sentence. And then the embeddings get passed to the decoder, which then decodes words one at a time.

What you'll notice here is that there are self-referential loops to the decoder. What I'm trying to visually communicate here is that the decoder is generating tokens one at a time, as we discussed. After it generates a token, that token will be passed back to the decoder, along with the rest of the input sequence to generate the next word, and so forth, until the entire sequence is generated.

At a glance, what I've done here is put together a table for your reference of various tasks and, historically, what style of model has been used to accomplish each task. One thing not to take away from this is that when you see a yes or no, that a particular model or a particular style of model must or cannot be used to perform a certain task.

You could, in theory, use any model to complete any task, but the pair may not be appropriate and is not traditionally done in practice. At a high level, the main takeaway here is that there are a variety of tasks that we could use language models for.

And different styles of models are deliberately selected to accomplish various tasks. This concludes our discussion on language model architectures. In the next lesson, we'll discuss affecting the model's distribution over tokens with a technique called prompting. 
