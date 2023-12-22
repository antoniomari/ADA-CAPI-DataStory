---
layout: page
title: Success or Failure?
subtitle: A comparative analysis of finished and unfinished Wikispeedia games
cover-img: /assets/img/network.jpg
---

Have you ever played a game and wanted to throw your phone against the wall? We have. That's why we want to look at all the ways players fail at [Wikispeedia](https://dlab.epfl.ch/wikispeedia/play/), a game in which the player navigates around a reduced version of Wikipedia (containing "just" 4'000 articles) to reach a target article from a starting article, only by clicking on hyperlinks. What makes people give up a game where they are searching for an elusive target in the forest of knowledge that is the Wikipedia graph? Did Wikispeedia let them down by giving them a way too difficult path, or is it your own fault?

<p align="center">
  <img src="assets/img/Sequence_2001.gif" alt="No"/>
</p>

Tolstoy said, “*Happy families are all alike; every unhappy family is unhappy in its own way*”. Similarly, finished paths are similar in the sense that they all reached their endpoint. However, unfinished paths could be unfinished due to a myriad of factors. Did the player give up because they grew tired of the game? Were they simply not familiar with the subject? Was the language too complicated for them? Did they get bored of the game? Frustrated? Annoyed? Or was the target nearly impossible to reach?

We embark to answer these questions. Through a range of (interactive) visualizations and witty conclusions, we will tell the story of wildly unfair article category choices, impossible-to-read articles, bottlenecks in the hyperlink structure and last but not least starring player skill gaps.

We believe that our findings could help game-style environments (e.g., online educational platforms) enhance player retention and satisfaction (e.g., by adjusting levels/tasks). Moreover, this analysis can also reveal valuable insights into the human psyche, determining potential deterring factors of completing a task.

### But before we dive in, what data are we working with?

Does Wikispeedia seem like an easy game to you? How often would you expect to lose? Our dataset is comprised of around **75'000 games and 33%** of them are unfinished. But do not be tricked!

{% include data_availability.html %}

Having a closer look at these paths, we see that the unfinished paths are only reported from 2011 onwards and by excluding the games prior to that point the **actual rate of unfinished paths becomes close to 52%**. Surprisingly, giving up is not a rare phenomenon, and this motivates the search for the reasons why players tend to give up.

**Each path shows us how people attempted to get from a starting article to a target article** through the forest of knowledge, successfully or not. As a complement to these paths, we have access to when they were played, how long the game lasted, the steps taken by the player, as well as the links between Wikipedia articles, the shortest path lengths between two articles, and the categories of the articles.

Also, a timeout limit of 3'600 seconds is set for each game. This means that a player can quit the game in two different ways: either restarting the game or reaching the timeout (which mostly happen when players close the webpage and end their session).

Now that we have an overview of the data, let's dive in! What are the main culprits in making players quit?

## Is math too hard?

We all know math is tough. We’d have a much nicer time reading a book, or poring over maps, instead of crying over our math homework. Could it be that we actually didn’t pay enough attention to math, so we cannot complete Wikispeedia games when they involve math subjects? More broadly, could it be that some categories are on average more difficult to navigate for some people, leading them to be lost in the forest of knowledge?

This is a possibility. To explore it, we first want to **understand the categories featured in the games** that Wikispeedia typically proposes to its players and how they relate to each other at a category level. Below, you can mess around with the **adjencency matrix which exactly represents these connections**, where the colours represent the strength between categories, based on the number of directed links between them. Go ahead, play with it, and let's see what kind of conclusions you can come up with!

{% include adjacency_matrix.html %}

This heatmap illustrates the difficulties associated with transitioning from specific categories. Did you notice that "Mathematics" articles have the fewest outgoing connections to other categories, and various categories rank "Mathematics" relatively low? (Hover over the nodes to see more details.) Take "Music," for instance, where only one article has a direct connection to math. On the other hand, it's clear which categories dominate the Wikipedia network. Geography stands out as the most prevalent category, with many articles linking it with the category itself. Considering a whopping 44.5% of geography articles hyperlinked to other geographical articles, one might think that transitioning into other categories would be a tough nut to crack. However, in absolute terms, Geography still has a substantial number of outgoing links to other categories, suggesting that moving around might be more straightforward, making it an easy game.

Nonetheless, to truly see the impact of categories on games, we need to do some further analysis. Let's first look at how the category of the target article can influence whether the game is completed or not. As you may recall, unfinished paths only became available in the dataset after 2011. However, to keep potential temporal fluctuations in game and player behaviour, we want to only look at the data from the period where we have both finished and unfinished paths.

Looking at this period, we can simply **estimate the likelihood of a game being unfinished, given the category of the target article**, using the empirical estimator; by looking at the number of games that were finished or unfinished with the given target article category.

{% include likelihood_target_category.html %}

That’s interesting… Turns out mathematics is the 5th easiest category to have as a target on average! It appears that we were paying attention after all, in spite of the complaints. Now it is clear how countries, geography, and religion could be relatively easier to reach compared to other categories, given the myriad of ways that players can make connections with them. But how could “everyday life” be such a difficult target to reach? Perhaps the whole story isn’t about whether we are familiar with the subjects we are dealing with. Perhaps there is more to it: maybe it is harder to reach some articles simply because of the nature of the Wikipedia graph. We’ll come back to this later.

In the meantime, let’s have a **deeper look into one of these categories, countries**, to show how there can be a good amount of variability within each of these fairly broad categories. We estimate the likelihood of reaching a specific target country in a similar fashion to the likelihoods before, but due to the lower availability of data per country, we use the add-1 estimator instead of the empirical estimator. We can then make a map from this data (Hooray!).

{% include countries.html %}

As we expect, some countries are more likely to be reached than others. And there is a significant variance in this, as **the probability of game completion given the target country ranges from a whole 93.3% to a measly 20%** (sorry, Uzbekistan). This highlights how there are still significant differences between target articles, even within the same broad category.

It should be noted that we looked into the role of starting article categories as well, but it was observed that their effect wasn’t as significant as that of the target article categories.

But anyway, let’s return to do one last investigation to shine more light on the role that categories play in games. We previously looked at the impact of categories in target articles. But there is a whole game before we reach the target. What if we **look at the pairings of start-target article categories** (and draw a beautiful plot in the process)?

Here, we color-coded the nodes based on their empirical likelihood of not reaching the categories as targets. Additionally, the edges are color-coded based on the difference in start-target article category between the finished and unfinished paths. Blue edges indicate that the start-target category pair occurs more frequently in the finished paths, possibly signifying an easier game. Conversely, red edges signify the opposite, that the start-target category pair was more prominent in the unfinished paths. Finally, gray edges (helping to highlight the main discrepancies) are those in which they appeared equally in both types of paths.

<div style="width: 100%; height=500px;">
  {% include finish-unfinish_category_strength.html %}
</div>

This fine-grained visualization of the difficulty levels associated with specific start-target category pairs (hover on different nodes to focus on its edges), allows to pinpoint particular scenarios where users didn't struggle or seemed to face challenges. Notably, the three blue nodes (i.e., Countries, Geography and Religion) all have a high number of incoming blue edges, which aligns with our analysis on their easiness as target articles. In comparison, "Everyday_life'' emerges as the most challenging target category, a finding that echoes our previous analysis.

While categories definitely influence how a game turns out, there are still some puzzling aspects. For instance, why don't other challenging categories (e.g., Business Studies, Citizenship, and Music) show any red edges? There is still a lot of unexplained variance, as we saw on our map comparing countries. Could there be something else in the articles to explain this? 

## The way we write

Before delving deep into the intricacies of the Wikispeedia gameplay, it's essential to explore another crucial aspect, the way information is presented within the articles.

We kicked off our analysis hoping that the article itself influences the player's path through the vast jungle of knowledge that is Wikispeedia. We tried to find commonalities in articles that players seemed to breeze through (the blue ones in the graph above) versus those that result in roadblocks (those red edges), expecting to be able to determine the factors which contribute to a user successfully completing a game or failing through the process, but no concrete evidence was found.

We focused our analysis on extracting features related to textual length (e.g., word count, average sentence length, etc.) and richness of information (e.g., stopword percentage, readability score, etc.) hoping these metrics could help us spot some disparities. When looking at articles metrics in different categories we found notable differences. For instance, Religion articles contain the largest word counts, whereas Science articles contain the shortest. Citizenship articles claim to rank lowest in readability score, while Everyday Life proved to be the easiest to read. However, **these metrics had no effect on finishing or not the game**. T-tests helped identify multiple significant differences between the start-target pairs in finished and unfinished paths, but their effect size is minimal.

While there might be other textual factors which might have an impact on the game, this doesn’t seem like the whole story. The way the content is written may not necessarily impact the game given that users only rely on hyperlinks to transition between articles. But what if the reason lies in the game itself?

## The game was too hard!

Ah yes. We’ve all heard it. “It’s not my fault, the game was too hard!” But in the case of Wikispeedia, do the complaints of gamers in need of a win actually hold ground? Are some games inherently harder than others? Well, it could be. How could this be the case?

Firstly, we observe that in order to reach a target, the target needs to have an incoming link in the Wikipedia graph. We further understand **intuitively that the more of these incoming links, the merrier**, giving the player multiple avenues to complete their search for the elusive target in the forest of knowledge. This is why we look at the distribution of the in-degrees of the target articles in finished and unfinished paths.

{% include in-degrees.html %}

This does look like a serious difference. The **target articles that were reached had an in-degree of 59.8 on average**, while that of the **target articles that were not reached was only 27.8**. Of course, any article can be reached or not depending on the game, but the collection of all these games played over the years does show a clear trend. This is further **confirmed by a t-test with a p-value of 0.000**, giving us the ability to reject the null hypothesis that the in-degrees of the target articles are statistically the same in the finished and unfinished paths.

We conjecture that the out-degrees of starting articles may result in a similar pattern, thinking that if the player has more ways to start their game, the more likely it would be that they can finish it. However, this does not come to be true, and we fail to reject the null in this case.

Nonetheless, we can make one more observation. Further broadening our investigation from looking at the roles of the start or target article only, we want to see if there is something in the pairings of the start and target articles that influences whether a game is finished or not. For this purpose, we ask: how easily could a computer solve this? The answer of course is given by the lengths of the shortest possible paths between the two articles. We thus look into the distribution of these lengths in finished and unfinished articles.

{% include shortest_path.html %}

This histogram is revealing. There is a clear difference in the two distributions, which is confirmed by a **t-test with a p-value of 0.000**, giving us the ability to reject the null hypothesis that the shortest possible path lengths are statistically the same in the finished and unfinished paths. In fact, the data shows that the shortest possible paths were **2.845 steps long on average in the finished paths**, while they were **3.232 steps long on average in the unfinished paths**.


## Putting it all together

But how do all of these individual effects stack up against each other? What ultimately has the biggest influence on earning the sweet spoils of victory - and what makes you throw down your phone in frustration? To study the combined effect, we **fit a logistic regression model** to understand which variables have which effect size. The dependent variable is the game status (with unfinished games as the positive class), while we use any variable discussed above that is known at the start of the game and independent of the player, grouped in 4 sections: Game Difficulty, Article Metrics as well as Starting and Target Categories.

![image](/assets/img/logistic_regression_coefficients.png)

We largely find our previous findings confirmed. By far the most important factor across all variable groups is the shortest possible path metric, indicating that **objective game difficulty truly plays a pivotal role**. Indeed, it might not be your fault if you horribly fail at a game of Wikispeedia. Similarly, more hyperlinks going into your target does make the job a lot easier.

**Linguistic article metrics do have very slight effects**, but are practically irrelevant compared to the other effects. This makes intuitive sense, most players do not actually read the articles, but rather Control-F or otherwise directly navigate to the hyperlink they were hoping to find.

Turning to the starting and target categories, we can see that the **target category generally has a larger effect size than the starting category**: It doesn't matter as much where one starts, as one can just navigate away. Further, while elusive and boring sounding categories like Language and Literature, Design and Technology and Everyday Life are hard to start and end up in, nerdy pages like Mathematics and IT seem to be fan favourites. Another interesting case is the category Geography: It’s always easy to reach a country (except maybe for Uzbekistan - sorry again); but it seems that starting the game from a country makes it quite hard to navigate away from it to the ultimate target article.

## Regressions are boring - Can’t we use a cooler model?

Sure we can! Through a more powerful model such as a Random Forest which considers non-linearities and interaction effects, we can even reach decent predictive performance. A basic first model already reaches an **F1-Score of 65.25%** and an overall **Accuracy of 65%**. But these figures per se are not that interesting; more interesting is using the **Shapley Values** (see e.g., [Molnar, 2019](https://christophm.github.io/interpretable-ml-book/shapley.html) for a good introduction) to explain why the model considers certain games as inherently harder.

For instance, consider the game where a player was asked to navigate from the UK Parliament to Latin America. Sounds pretty easy, right? Our model tends to agree:

![image](/assets/img/shapley_easy_game_2.png)

The plot shows a few things. First, the predicted probability of the player giving up is merely 25%, whereas the base value (average in the dataset) is slightly above 50%. Further, it shows that the target category being Geography, the very short shortest path length as well as the many links going into Latin America are mainly responsible for the low predicted probability.

What about a game from the Industrial Revolution to the Legend of Zelda Video Game Series?

![image](/assets/img/shapley_harder_game_2.png)

The model predicts that the player stands no chance. Only two hyperlinks point to the target – good luck finding any of those! Also, the target category and the relatively long optimal path through the network increased the odds of quitting. Indeed, it took 61 Wikipedia articles, before the player finally decided to give up - our model was right.

## Ultimately, it all comes down to you

Thus far, we have looked at the game, the machine, the network, but missed one of the most crucial parts of the story: the individual player and their behaviour.

### Never turn back...
The way you play tells more than you think! No one is spying on you while you’re playing, but you’re leaving virtual breadcrumbs behind while you walk through Wikispeedia.

One example? The more you hit that back button during navigation, the likelier you are to throw in the towel.

If we group all the finished and unfinished games played by each user, and compute how frequently on average they use the back click button, we’d observe a clear distinction in the probability of frequent back-clicking. The below plot shows in fact that for **finished games the frequency of back clicks is limited and rarely over 0.3, meaning that it’s unlikely that a player that back clicks too often will finish that game.**

{% include backclick_distr.html %}

When do we back click? Well, sometimes we think to know about certain subjects more than we actually do. 

As you can see in the below barchart, the back click rate for different categories, i.e. how frequently we leave a page of that category using the back click over the total number of times a page of the same category is visited, may be **very different from category to category**, and again, it’s statistically significantly different between finished and unfinished games.

{% include backclick_cat.html %}

### ...and never give up!

But wait, there's more!

We peeked into the **semantic similarity between the pages players travel through and the ultimate target** and it looks like for those who make it to the finish line, the average similarity to the target starts getting higher than the one achieved by quitters after a certain threshold. It’s interesting to notice that this threshold increases while we increase the length of the paths analyzed, showing how players that ended up in long paths but still managed to finish really had to hang in there for long!

This line plot shows the **trend of the semantic similarity of the current page to the title of the target page**, during the progress of the game. Games of equal length are shown in the same frame. You can play with this interactive plot by choosing the length of the paths to consider and see how players who didn't give up despite long paths, finally saw the light and started rapidly getting closer to the target.


{% include semantic_sim_vs_progress.html %}


## That’s cool and all, but why should I care?
Good question! **Game designers can use these factors to add different difficulty levels or to make the overall game more satisfying and rewarding** by proposing games that are balanced across the most influential factors in predicting game difficulties. Further, our machine learning model predicts a probability which could also directly be used to create various difficulty levels (e.g., easy, medium and hard) from which players can choose.

Along the same vein, we could expand our ML model to predict a quitting probability on each page that a player lands at. At first glance, this seems to work quite well by leveraging individual player behaviour (using the semantic distance measure discussed above) along with all other factors(see the notebook for a proof of concept). Such a model could be used to give hints to players when they are close to quitting.

## Summing up

All of these measures could **help improve player satisfaction and retention**, which ultimately are the end-goal of any (profit-seeking or in the case of Wikispeedia, data-seeking) organization. Companies (Game Developers or not) spend billions each year trying to glue users to the phone or computer screen, all in order to sell them more in-game upgrades or show them more ads.

What started out as a quest to understand why humans tend to throw their phones, turned out to be quite useful for game designers. Through a range of visual analyses, we learned that:
- Some article categories are much worse connected than others - leading to “dark areas” in the Wikispeedia network that are hard to reach. For instance, Geography articles are very easy to reach, while categories like “Language and Literature” are much harder.
- Similar, albeit smaller effects exist for the starting category, where for some it’s easier to successfully navigate away to the target than for others.
- While differences in the way articles are written exists between categories, this has basically no effect on whether a player finishes a game.
- The game difficulty (as measured by the length of the optimal path and the links going into the target article) has by far the biggest effect on players giving up.
- Additionally, players behaved and navigated differently in games they finished vs. in games they did not finish.
- Moreover, players only got semantically close to the target in the few final clicks of their game before reaching the target itself.

Finally, we showed that these findings can be used by game designers to improve player retention and satisfaction, for instance through predictive ML models - hopefully slightly lowering the number of rage quitting players (and broken phones) in the future.
