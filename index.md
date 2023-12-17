---
layout: page
title: Success or Failure?
subtitle: A comparative analysis of finished and unfinished Wikispeedia games
cover-img: /assets/img/mountains.jpg
---

Have you ever played a game and wanted to throw your phone against the wall? We have. That's why we want to look at all the ways players fail at Wikispeedia. What makes people give up a game? Did Wikispeedia let them down by giving them a way too difficult path, or is it your own fault?

Tolstoy said, “Happy families are all alike; every unhappy family is unhappy in its own way.” Similarly, finished paths are similar in the sense that they all reached their endpoint. However, unfinished paths could be unfinished due to a myriad of factors. Did the player give up because they grew tired of the game? Were they simply not familiar with the subject? Was the language too complicated for them? Did they get bored of the game? Frustrated? Annoyed? Or was the target nearly impossible to reach? 

We embark to answer these questions. Through a range of (interactive) visualizations and witty conclusions, we will tell the story of wildly unfair article category choices, impossible-to-read articles, bottlenecks in the hyperlink structure and last but not least starring player skill gaps.

We believe that our findings could help game-style environments (e.g., online educational platforms) enhance player retention and satisfaction (e.g., by adjusting levels/tasks). Moreover, this analysis can also reveal valuable insights into the human psyche, determining potential deterring factors of completing a task.

But before we dive in, what data are we working with?

We have access to many finished and unfinished paths across time. These paths show us how people attempted to get from a starting article to a target article, successfully or not. As a complement to these paths, we have access to when they were played, how long the game lasted, the steps taken by the player, as well as the links between Wikipedia articles, the shortest path lengths between two articles, and the categories of the articles.

Using this data, we explore which explanatory suspects could be the most important culprits leading to the player’s unsuccessful game in the analysis below.

## Is math too hard?

We all know math is tough. We’d have a much nicer time reading a book, or poring over maps, instead of crying over our math homework. Could it be that we actually didn’t pay enough attention to math, so we cannot complete Wikispeedia games when they involve math? More broadly, could it be that some categories are on average more difficult to navigate for some people? 

This is a possibility. To explore it, we first want to know the categories involved in the games that Wikispeedia typically proposes to its players.

<div style="width: 100%; height=500px;">
  {% include article_category_strength.html %}
</div>

Talk about this

OK, now that we know that, we can look at how the category of the target article can influence whether the game is completed or not. Let’s check the distribution of finished and unfinished articles over time:

{% include data_availability.html %}

It appears that we don’t have unfinished paths before a certain date. To keep potential temporal fluctuations in game and player behaviour, we want to only look at the data from the period where we have both finished and unfinished paths.

Looking at this period, we can simply estimate the likelihood of a game being unfinished, given the category of the target article, using the empirical estimator; by looking at the number of games that were finished or unfinished with the given target article category.

{% include likelihood_target_category.html %}

That’s interesting… Turns out mathematics is the 5th easiest category to have as a target on average! It appears that we were paying attention after all, in spite of the complaints. Now it is clear how countries, geography, and religion could be relatively easier to reach compared to other categories, given the myriad of ways that players can make connections with them. But how could “everyday life” be such a difficult target to reach? Perhaps the whole story isn’t about whether we are familiar with the subjects we are dealing with. Perhaps there is more to it: maybe it is harder to reach some articles simply because of the nature of the Wikipedia graph. We’ll come back to this later.

In the meantime, let’s have a deeper look into one of these categories, countries, to show how there can be a good amount of variability within each of these fairly broad categories. We estimate the likelihood of reaching a specific target country in a similar fashion to the likelihoods before, but due to the lower availability of data per country, we use the add-1 estimator instead of the empirical estimator. We can then make a map from this data (Hooray!).

{% include countries.html %}

As we expect, some countries are more likely to be reached than others. And there is a significant variance in this, as the probability of game completion given the target country ranges from a whole 93.3% to a measly 20% (sorry, Uzbekistan). This highlights how there are still significant differences between target articles, even within the same broad category.

But anyway, let’s return to do one last investigation to shine more light on the role that categories play in games. We previously looked at the impact of categories in target articles. But there is a whole game before we reach the target. What if we look at the pairings of start and target article categories (and draw a beautiful plot in the process)?

<div style="width: 100%; height=500px;">
  {% include finish-unfinish_category_strength.html %}
</div>

Talk about this

Well, ok. The categories clearly play a role in the outcome of a  game. But there is still a lot of unexplained variance, as we saw on our map. There may be something else in the articles to explain this. In fact, we should really talk about what is in the articles.

## The way we write

Talk about article metrics

While this is interesting to observe, and there were definitely some factors that had a fairly significant impact on the game, this doesn’t seem like the whole story. What if the answers that we are looking for are not in individual articles, but the Wikipedia network that connects them?

## The game was too hard!

Ah yes. We’ve all heard it. “It’s not my fault, the game was too hard!” But in the case of Wikispeedia, do the complaints of gamers in need of a win actually hold ground? Are some games inherently harder than others? Well, it could be. How could this be the case?

Firstly, we observe that in order to reach a target, the target needs to have an incoming link in the Wikipedia graph. We further understand intuitively that the more of these links, the merrier, giving the player multiple avenues to fulfil their search for the elusive target. This is why we look at the distribution of the in-degrees of the target articles in finished and unfinished paths.

{% include in-degrees.html %}

This does look like a serious difference. The target articles that were reached had an in-degree of 59.8 on average, while that of the target articles that were not reached was only 27.8. Of course, any article can be reached or not depending on the game, but the collection of all these games played over the years does show a clear trend. This is further confirmed by a t-test with a p-value of 0.000, giving us the ability to reject the null hypothesis that the in-degrees of the target articles are statistically the same in the finished and unfinished paths.

We conjecture that the out-degrees of starting articles may result in a similar pattern, thinking that if the player has more ways to start their game, the more likely it would be that they can finish it. However, this does not come to be true, and we fail to reject the null in this case.

Nonetheless, we can make one more observation. Further broadening our investigation from looking at the roles of the start or target article only, we want to see if there is something in the pairings of the start and target articles that influences whether a game is finished or not. For this purpose, we ask: how easily could a computer solve this? The answer of course is given by the lengths of the shortest possible paths between the two articles. We thus look into the distribution of these lengths in finished and unfinished articles.

{% include shortest_path.html %}

This histogram is revealing. There is a clear difference in the two distributions, which is confirmed by a t-test with a p-value of 0.000, giving us the ability to reject the null hypothesis that the shortest possible path lengths are statistically the same in the finished and unfinished paths. In fact, the data shows that the shortest possible paths were 2.845 steps long on average in the finished paths, while they were 3.232 steps long on average in the unfinished paths.

All of the analyses above are promising, and could help in the explanation for why people give up once we unify them in regression and through machine learning. However, there is one last thing we want to look at before we do this. Thus far, we have looked at the game, the machine, the network, but missed one of the most crucial parts of the story: the individual player, and how they behave. We have to look at that too.

## It all comes down to you

Talk about player behaviour

## Regression

To combine all of these individual factors, we estimate a logistic regression, modeling whether a game has been finished using the article category, article metrics, objective difficulty measures (shortest path).

We largely find our previous findings confirmed. By far the most important factor is the shortest possible path metric, indicating that objective game difficulty indeed plays a pivotal role. ADD INTERPRETATION. Evidently, some categories do make games harder or easier (e.g., Mathematics is apparently easier than Every Day Life), while individual article metrics are statistically significant but with a very low effect size.

## Machine learning

Through a more powerful model such as a Random Forest which considers non-linearities and interaction effects, we can even reach decent predictive performance. A basic first model already reaches F1-Scores of 56% and an overall Accuracy of 70%. But these figures per se are not that interesting; more interesting is using the Shapley Values to explain why the model considers certain games as inherently harder.

For instance, this one player took 423 clicks to the target. Needless to say that he sucked, but was the path actually harder than others? Our model can provide the answer:

OUTPUT: Shapley values for chosen games.

Also, this player found the target in 3 steps; would others have struggled more?

OUTPUT: Shapley values for chosen games.

A game designer can use these factors to add different difficulty levels or make the overall game more balanced by choosing games that are balanced across the most influential factors in predicting game difficulties.
Similarly, leveraging the insights from this piece, we can build an ML model to estimate the probability of quitting on every page as the game progresses. See the proof of concept in the notebook here (LINK). The semantic distance measure from part XYZ proves to be quite predictive, which makes sense considering the plot. Such a model could be used to give players hints on the pages where the quitting probability is high, thereby reducing attrition and playing time.

What started out as a quest to understand why humans tend to throw their phones (change), turned out to be quite useful for game designers. Through a range of visual analyses, we learned that:
Bullet Summary 1
Bullet Summary 2
Bullet Summary 3

Finally, through predictive models, we provide insights and tools to improve the game design of Wikispeedia - hopefully slightly lowering the number of rage quitting players in the future.