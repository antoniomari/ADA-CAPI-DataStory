---
layout: page
title: Success or Failure?
subtitle: A comparative analysis of finished and unfinished Wikispeedia games
cover-img: /assets/img/network.jpg
---

<div style="text-align: justify"> 

Have you ever played a game and wanted to throw your phone against the wall? We have. That's why we want to look at all the ways players fail at Wikispeedia. What makes people give up a game where they are searching for an elusive target in the forest of knowledge that is the Wikipedia graph? Did Wikispeedia let them down by giving them a way too difficult path, or is it your own fault?

Tolstoy said, “*Happy families are all alike; every unhappy family is unhappy in its own way*”. Similarly, finished paths are similar in the sense that they all reached their endpoint. However, unfinished paths could be unfinished due to a myriad of factors. Did the player give up because they grew tired of the game? Were they simply not familiar with the subject? Was the language too complicated for them? Did they get bored of the game? Frustrated? Annoyed? Or was the target nearly impossible to reach? 

We embark to answer these questions. Through a range of (interactive) visualizations and witty conclusions, we will tell the story of wildly unfair article category choices, impossible-to-read articles, bottlenecks in the hyperlink structure and last but not least starring player skill gaps.

We believe that our findings could help game-style environments (e.g., online educational platforms) enhance player retention and satisfaction (e.g., by adjusting levels/tasks). Moreover, this analysis can also reveal valuable insights into the human psyche, determining potential deterring factors of completing a task.

**But before we dive in, what data are we working with?**

We have access to many finished and unfinished paths across time. These paths show us how people attempted to get from a starting article to a target article through the forest of knowledge, successfully or not. As a complement to these paths, we have access to when they were played, how long the game lasted, the steps taken by the player, as well as the links between Wikipedia articles, the shortest path lengths between two articles, and the categories of the articles.

Using this data, we explore which explanatory suspects could be the most important culprits leading to the player’s unsuccessful game in the analysis below.

## Is math too hard?

We all know math is tough. We’d have a much nicer time reading a book, or poring over maps, instead of crying over our math homework. Could it be that we actually didn’t pay enough attention to math, so we cannot complete Wikispeedia games when they involve math? More broadly, could it be that some categories are on average more difficult to navigate for some people, leading them to be lost in the forest of knowledge? 

This is a possibility. To explore it, we first want to understand the categories featured in the games that Wikispeedia typically proposes to its players and how they relate to each other at a category level. Below, you can mess around with the graph which exactly represents these connections, where the edge widths represent the strength between categories. Go ahead, play with it, and let's see what kind of conclusions you can come up with!

<div style="width: 100%; height=500px;">
  {% include article_category_strength.html %}
</div>

This first graph illustrates the difficulties associated with transitioning from specific categories. Did you notice that "Mathematics" articles have the fewest outgoing connections to other categories, and various categories rank "Mathematics" relatively low? (Hover the nodes to see more details) Take "Music," for instance, where only one article has a direct connection to math. On the other hand, it's clear which categories dominate the Wikipedia network. Geography stands out as the most prevalent category, with many articles linking it with the category itself. Considering a whopping 44.5% of geography articles hyperlinked to other geographical articles, one might think that transitioning into other categories would be a tough nut to crack. However, in absolute terms, Geography still has a substantial number of outgoing links to other categories, suggesting that moving around might be more straightforward, making it an easy game.

OK, now that we know that, we can look at how the category of the target article can influence whether the game is completed or not. Let’s check the distribution of finished and unfinished articles over time:

{% include data_availability.html %}

It appears that we don’t have unfinished paths before a certain date. To keep potential temporal fluctuations in game and player behaviour, we want to only look at the data from the period where we have both finished and unfinished paths.

Looking at this period, we can simply estimate the likelihood of a game being unfinished, given the category of the target article, using the empirical estimator; by looking at the number of games that were finished or unfinished with the given target article category.

{% include likelihood_target_category.html %}

That’s interesting… Turns out mathematics is the 5th easiest category to have as a target on average! It appears that we were paying attention after all, in spite of the complaints. Now it is clear how countries, geography, and religion could be relatively easier to reach compared to other categories, given the myriad of ways that players can make connections with them. But how could “everyday life” be such a difficult target to reach? Perhaps the whole story isn’t about whether we are familiar with the subjects we are dealing with. Perhaps there is more to it: maybe it is harder to reach some articles simply because of the nature of the Wikipedia graph. We’ll come back to this later.

In the meantime, let’s have a deeper look into one of these categories, countries, to show how there can be a good amount of variability within each of these fairly broad categories. We estimate the likelihood of reaching a specific target country in a similar fashion to the likelihoods before, but due to the lower availability of data per country, we use the add-1 estimator instead of the empirical estimator. We can then make a map from this data (Hooray!).

{% include countries.html %}

As we expect, some countries are more likely to be reached than others. And there is a significant variance in this, as the probability of game completion given the target country ranges from a whole 93.3% to a measly 20% (sorry, Uzbekistan). This highlights how there are still significant differences between target articles, even within the same broad category.

It should be noted that we looked into the role of starting article categories as well, but it was observed that their effect wasn’t as significant as that of the target article categories.

But anyway, let’s return to do one last investigation to shine more light on the role that categories play in games. We previously looked at the impact of categories in target articles. But there is a whole game before we reach the target. What if we look at the pairings of start-target article categories (and draw a beautiful plot in the process)?

Here, we color-coded the nodes based on their empirical likelihood of not reaching the categories as targets. Additionally, the edges are color-coded based on the difference in start-target article category between the finished and unfinished paths. Green edges indicate that the start-target category pair occurs more frequently in the finished paths, possibly signifying an easier game. Conversely, red edges signify the opposite, that the start-target category pair was more prominent in the unfinished paths. Finally, gray edges (helping to highlight the main discrepancies) are those in which they appeared equally in both types of paths.

<div style="width: 100%; height=500px;">
  {% include finish-unfinish_category_strength.html %}
</div>

This fine-grained visualization of the difficulty levels associated with specific start-target category pairs (hover on different nodes to focus on its edges), allows to pinpoint particular scenarios where users didn't struggle or seemed to face challenges. Notably, the three green nodes (i.e., Countries, Geography and Religion) all have a high number of incoming green edges, which aligns with our analysis on their easiness as target articles. In comparison, "Everyday_life'' emerges as the most challenging target category, a finding that echoes our previous analysis.

While categories definitely influence how a game turns out, there are still some puzzling aspects. For instance, why don't other challenging categories (e.g., Business Studies, Citizenship, and Music) show any red edges? There is still a lot of unexplained variance, as we saw on our map comparing countries. Could there be something else in the articles to explain this? In fact, we should really talk about what is in the articles.

## The way we write

Talk about article metrics

While this is interesting to observe, and there were definitely some factors that had a fairly significant impact on the game, this doesn’t seem like the whole story. What if the answers that we are looking for are not in individual articles, but the Wikipedia network that connects them?

## The game was too hard!

Ah yes. We’ve all heard it. “It’s not my fault, the game was too hard!” But in the case of Wikispeedia, do the complaints of gamers in need of a win actually hold ground? Are some games inherently harder than others? Well, it could be. How could this be the case?

Firstly, we observe that in order to reach a target, the target needs to have an incoming link in the Wikipedia graph. We further understand intuitively that the more of these links, the merrier, giving the player multiple avenues to complete their search for the elusive target in the forest of knowledge. This is why we look at the distribution of the in-degrees of the target articles in finished and unfinished paths.

{% include in-degrees.html %}

This does look like a serious difference. The target articles that were reached had an in-degree of 59.8 on average, while that of the target articles that were not reached was only 27.8. Of course, any article can be reached or not depending on the game, but the collection of all these games played over the years does show a clear trend. This is further confirmed by a t-test with a p-value of 0.000, giving us the ability to reject the null hypothesis that the in-degrees of the target articles are statistically the same in the finished and unfinished paths.

We conjecture that the out-degrees of starting articles may result in a similar pattern, thinking that if the player has more ways to start their game, the more likely it would be that they can finish it. However, this does not come to be true, and we fail to reject the null in this case.

Nonetheless, we can make one more observation. Further broadening our investigation from looking at the roles of the start or target article only, we want to see if there is something in the pairings of the start and target articles that influences whether a game is finished or not. For this purpose, we ask: how easily could a computer solve this? The answer of course is given by the lengths of the shortest possible paths between the two articles. We thus look into the distribution of these lengths in finished and unfinished articles.

{% include shortest_path.html %}

This histogram is revealing. There is a clear difference in the two distributions, which is confirmed by a t-test with a p-value of 0.000, giving us the ability to reject the null hypothesis that the shortest possible path lengths are statistically the same in the finished and unfinished paths. In fact, the data shows that the shortest possible paths were 2.845 steps long on average in the finished paths, while they were 3.232 steps long on average in the unfinished paths.

All of the analyses above are promising, and could help in the explanation for why people give up once we unify them in regression and through machine learning. However, there is one last thing we want to look at before we do this. Thus far, we have looked at the game, the machine, the network, but missed one of the most crucial parts of the story: the individual player, and how they behave. We have to look at that too.

## It all comes down to you

Talk about player behaviour

#### Backclick
{% include backclick_distr.html %}


{% include backclick_cat.html %}

#### Semantic

{% include avg_semantic_sim_distr.html %}

{% include semantic_sim_vs_progress.html %}


## Putting it all together

But how do all of these individual effects stack up against each other? What ultimately has the biggest influence on earning the sweet spoils of victory - and what makes you throw down your phone in frustration? To study the combined effect, we fit a Logistic regression model to understand which variables have which effect size. The dependent variable is the game status (with unfinished games as the positive class), while we use any variable discussed above that is known at the start of the game and independent of the player, grouped in 4 sections: Game Difficulty, Article Metrics as well as Starting and Target Categories.

![image](/assets/img/logistic_regression_coefficients.png)

We largely find our previous findings confirmed. By far the most important factor across all variable groups is the shortest possible path metric, indicating that objective game difficulty truly plays a pivotal role. Indeed, it might not be your fault if you horribly fail at a game of Wikispeedia. Similarly, more hyperlinks going into your target does make the job a lot easier. 

Linguistic article metrics do have very slight effects, but are practically irrelevant compared to the other effects. This makes intuitive sense, most players do not actually read the articles, but rather Control-F or otherwise directly navigate to the hyperlink they were hoping to find.

Turning to the starting and target categories, we can see that the target category generally has a larger effect size than the starting category: It doesn't matter as much where one starts, as one can just navigate away. Further, while elusive and boring sounding categories like Language and Literature, Design and Technology and Everyday Life are hard to start and end up in, nerdy pages like Mathematics and IT seem to be fan favorites. Another interesting case is the category Geography: It’s always easy to reach a country (except maybe for Uzbekistan - sorry again); but it seems that starting the game from a country makes it quite hard to navigate away from it to the ultimate target article. 


## Regressions are boring - Can’t we use a cooler model?

Sure we can! Through a more powerful model such as a Random Forest which considers non-linearities and interaction effects, we can even reach decent predictive performance. A basic first model already reaches F1-Scores of 65.25% and an overall Accuracy of 65%. But these figures per se are not that interesting; more interesting is using the Shapley Values (see e.g., Molnar, 2019 <<[can add a link here perhaps]>> for a good introduction) to explain why the model considers certain games as inherently harder. 

For instance, consider the game where a player was asked to navigate from the UK Parliament to  Latin America. Sounds pretty easy, right? Our model tends to agree:

![image](/assets/img/shapley_easy_game_2.png)

The plot shows a few things. First, the predicted probability of the player giving up is merely 25%, whereas the base value (average in the dataset) is slightly above 50%. Further, it shows that the target category being Geography, the very short shortest path length as well as the many links going into Latin America are mainly responsible for the low predicted probability.

What about a game from the Industrial Revolution to the Legend of Zelda Video Game Series? 

![image](/assets/img/shapley_harder_game_2.png)

The model predicts that the player stands no chance. Only two hyperlinks point to the target – good luck finding any of those! Also, the target category and the relatively long optimal path through the network increased the odds of quitting. Indeed, it took 61 Wikipedia articles, before the player finally decided to give up - our model was right.

## That’s cool and all, but why should I care?
Good question! Game designers can use these factors to add different difficulty levels or make the overall game more satisfying and rewarding by proposing games that are balanced across the most influential factors in predicting game difficulties. Further, our predicted probability could also be used to create various difficulty levels (e.g., easy, medium and hard) from which players can choose.

Along the same vein, we could expand the ML model to predict a quitting probability on each page that a player lands at. At first glance, this seems to work quite well by using the semantic distance measure discussed above (see the notebook for a proof of concept). Such a model could be used to give hints to players when they are close to quitting.

All of these measures could help improve player satisfaction and retention, which ultimately are the end-goal of any (profit-seeking or in the case of Wikispeedia, data-seeking) organization. Companies (Game Developers or not) spend billions each year trying to glue users to the phone or computer screen, all in order to sell them more in-game upgrades or show them more ads.

Thus, our quest to understand why humans tend to give up in a relatively simple game could help game designers improve their games, and give insights into the ways that we tend to think. Through a range of visual analyses, we learned that:
- There are gaps in our collective knowledge, such as in the area of language and literature.
- The biggest denominator in terms of whether a game will be finished or not is the difficulty presented by the game structure itself.
- Players tend to give up when they are far from the target, and showcase indicative behaviours before doing so

Finally, through predictive models, we provide insights and tools to improve the game design of Wikispeedia - hopefully slightly lowering the number of rage quitting players (and broken phones) in the future.


</div>