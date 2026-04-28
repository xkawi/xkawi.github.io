---
title: "My 'accidental' early exposure to AI"
date: 2026-04-28
description: ""
tags: [AI, Supervised Learning, Naive Bayes Classifier, Token]
---

Long story short, I was actually exposed to "AI" back in 2011 without me realising it. It was a Final Year Project during my Diploma time when my friends and I implemented a Supervised Learning algorithm called Naive Bayes Classifier. The project was simple: first, train the model with a preset of data with labels (negative tweet, neutral, or positive tweet), and then fetch all the tweets for a given user and classify each tweet using the trained model if they are negative or positive.

Let's expand a little bit more on the project itself.

The problem statement is simple: given a public Twitter account (e.g. a school handle), we want to analyse their tweets timeline and classify if they appear to be giving negative sentiments or positive, or neutral and observe the distributions of those sentiments whether negative has higher count than positive.

The first order of business is of course to train the classifier model. We were tasked to implement the model using Naive Bayes Classifier, which is a supervised learning algorithm. Consequently, we prepared a set of training data, which is a list of texts with labels for each of them (e.g. "f*** off" labelled as 'negative'). For the actual training logic, we implemented it in Node.js with the help of [Natural](https://www.npmjs.com/package/natural?activeTab=dependencies) npm package. At the end of the training run, it outputs a `classifier.json` file, which is then used to classify each tweet. There were also stop words that we had to feed into the model, and also the concept of tokenizing the tweets into words, and many more. For more details on how the algorithm works, the [documentation](https://naturalnode.github.io/natural/bayesian_classifier.html) will do a much better job than me.

Last but not least, we had to implement the tweets fetching itself. This is pretty straightforward: use a Twitter API library, set up the necessary authentication, and then use the library to fetch the tweets (e.g. `Twit().fetchTimelines()`). Then we just loop through each tweet, and feed it into the trained model to be classified, and then we saved those results into a file for manual review.

You can inspect how we implemented it here - https://github.com/xkawi/Twitelizer (please pardon the newbie mistakes like committing the node_modules and API keys 😅).

As simple as it may sound, imo, that experience and knowledge gained now serve me well in navigating the new realm of AI to at least know what I do not know yet, and am able to figure out what I should learn next. The rest of the knowledge gaps now feel easier to fill in, for example:
1. tokenization relates to context size, hence reducing the context size means we should reduce the number of tokens to process
2. another example: yes, there are pre-trained models out there for specific use case X ready to use, but what if I want to customize it to use case Y? well, we have to go through the training process again, and then it is actually much easier now to train models with tools like Google's Vertex AI
3. AI models are just like the classifier.json file I mentioned above, just that it operates on a much larger data size, hence it is called Large-Language Model, but the fundamentals remain the same.

Having said that, there is still a lot I have to learn and am still curious about on how it works/implemented, one of them being, how video generation actually works under the hood? As fascinating as it appears to be, I still have no clue about the underlying technology behind it.

In retrospect, iirc, this Sentiment Analysis project was one of the few projects available for selection, and eventually we were assigned to it. We felt excited yet worried at the same time about the challenging project, because from a student's perspective, the project requirements actually appeared to be quite complex and challenging, which of course could affect our grade if we could not deliver.

Luckily we had a good project sponsor and mentor to guide us throughout. It was indeed challenging, but we managed to deliver and were given a good grade, which I suspect was mainly for our effort too, not necessarily due to the quality of the deliverable (because the code is really not that great, hah.)

And fast forward to today, I am really glad for that "accidental" exposure (partly because back then the project was categorised as "machine learning" rather than "artificial intelligence"), because now the knowledge gained is proven to be useful for me to quickly get up to speed on the AI train.

Key takeaway? Stay curious, keep learning, as you never know when it will come in handy!

Cheers!