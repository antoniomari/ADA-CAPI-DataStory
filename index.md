---
layout: page
title: OUR TITLE OF THE STORY
subtitle: OUR SUBTITLE (e.g., An analysis on gender bias)
cover-img: /assets/img/landscape_wiki2.png
---

Have you ever played a game and wanted to throw your phone against the wall? We have. That's why we want to look at all the ways players fail at Wikispeedia. What makes people give up a game? Did Wikispeedia let them down by giving them a way too difficult path, or is it your own fault?

We embark to answer these questions. Through a range of (interactive) visualizations and witty conclusions, we will tell the story of wildly unfair article category choices, impossible to read articles, bottlenecks in the hyperlink structure and last but not least starring player skill gaps.

Maybe So-What here?: These pieces of information can help xyz.

But before we dive in, what data are we working with?

{% include_relative likelihood_target_category.html %}

*Data Part.*
...
*Player Skill Gap.*

{% include likelihood_target_category.html %}

To combine all of these individual factors, we estimate a logistic regression, modeling whether a game has been finished using the article category, article metrics, objective difficulty measures (shortest path).

We largely find our previous findings confirmed. By far the most important factor is the shortest possible path metric, indicating that objective game difficulty indeed plays a pivotal role. ADD INTERPRETATION. Evidently, some categories do make games harder or easier (e.g., Mathematics is apparently easier than Every Day Life), while individual article metrics are statistically significant but with a very low effect size.

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








Data story structure & planning

Intro:
- Have you ever played a game and wanted to throw your phone against the wall? We have. That's why we want to look at all the ways players fail at Wikispeedia. What makes people give up a game? Did Wikispeedia let them down by giving them a way too difficult path, or is it your own fault?
- Make fun of the guy who played a game that is insanely long

Data exploration:
Availability of data over time:
Data between 2008 and 2014
No unfinished games before 2011
More exploration pertinent?

So then we may want to first look at what categories people find hardest to work with.
We first look here at how the articles are interconnected at a category level (through Juan graph 1)
Talk about how some categories are more connected than others (this can be seen when hovering - displays the total incoming and outgoing edge sums)
E.g., Mathematics vs Geography (wider edges)
Talk about how some categories are strongly interconnected to themselves (and to a limited number of other categories)
E.g. Geography/Science seem to be strongly connected to themselves
E.g. Geography to Science/Countries/People/History/Citizenship (easy to reach those articles)
TODO: Interactive??


Then we can explore how different categories of targets are more difficult
Countries in particular is very easy, it seems as if people can connect to countries in many ways
On the other hand, many topics are considered hard, with a likelihood of failure above 50%
The 95% error bars further indicate that some of these differences are statistically significant
The easier topics tend to be more “general knowledge”, whereas the harder topics are more specific. Interestingly, everyday life is also there. This may be because the topics are considered very widespread and thus not linked to by many wikipedia articles
Of course, categories are an oversimplification. Zooming in on countries, we can see that some countries are easier to reach than others
Finally we can show the difference in strength between the connection of starting article category (starting node) and target article category (where the outgoing edge points) in the finished/unfinished paths (Juan graph 2)
Node colors:
Based on the category difficulty (Arda’s plot)
Edge colors:
Green: the start-target category link appeared more in the finished paths (“easy”, known to be solvable)
Red: the start-target category link appeared more in the unfinished paths (“harder”)
Gray: the start-target category link (an edge) is equally likely to be reached in finished and unfinished paths
Finer grained visualization of the hardness of certain start/target articles (here based on categories)
Reassures that e.g. having “Everyday_life” as a target makes the game very hard


Articles textual content: ??
Do we want to mention that we had a look at different metrics to evaluate if articles in different categories had significant differences? And then conclude that although differences were found across the different categories we were unable to link it to being able to finish or not the game.

But apart from categories, which are an example of a factor that is somewhat subjective, what objective factors could determine the ease of a game?
Intuitively, if a target has many links pointing to it in the wikipedia graph, a.k.a. A large in-degree, then it should be easier to reach. Indeed this is true!
In-degrees follow a log-normal distribution
The targets that were reached had an in-degree of 59.809 on average, whereas the targets that were not reached had an in-degree of 27.773 on average. This is a very big difference. (OR SHOULD DO MEDIAN?)
A t-test confirms this statistically, p-value of 0.000
The same sort of impact is not achieved by the out-degree of starting articles, even though it was expected that it would.
Similarly, having a shorter possible path to win the game should make it easier to do so. We thus look at shortest possible path lengths for the games, and realise that this is indeed the case
Mention impossible paths?
The shortest possible paths were 2.845 long on average in the finished paths. The shortest possible paths were 3.232 long on average in the unfinished paths. While the difference is small, this could have a large impact on the completion of a game
A t-test confirms this statistically, p-value of 0.000


TO BE TALKED ABOUT: How to reconcile the fact that target category and target in-degree seem to be related:

Or do we just ignore it
Or do we mention (without going into details) that while they may be related, we believe that the two can still provide valuable information.
Technically the two seem to be acting as confounders to each other… but we were told no causal analysis needed








Putting it all together:


Mention the following things:
Articles category have high confidence bands, yet some are statistically relevant, conforming to the graph plots shown above)
Article metrics significant, but no big effect
Finally, shortest path by far biggest influence → some games are actually just harder than others (we can tie that in to the storyline, it is not the player’s but rather the game’s fault)

With an ML model in the backend, we can also produce indidivudal shapley explanations for why a game is hard or easy (embedded model, so it outputs this plot, if this is somehow possible).

We also went on to explore the semantic distance more closely in regards to its predictive power whether a game will be abandon at a specific page. For this we build a model with the per page observation as samples. We reach very high F1-Scores, with semantic distances being the discerning factor.
TO-DISCUSS: this seems too good to be true (F1-Scores of 96%), do we have data leakage somewhere with the semantic distance measure? Is it fair game to use that for predictions?
