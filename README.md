# First Analysis of pass patterns by teams and players in the World Cup 2022 using StatsBomb free data
In this repository I'll use StatsBomb free data from the WC2022 to make an initial analysis of pass patterns by teams and players. In particular, I'll try to find the best teams in set pieces and the most decisive players in regular plays. 

## Introduction
Football is a sport that has been played for centuries, but it's only in recent years that it has become a hotbed for analytics and data-driven insights. Now, teams and coaches are using data to drive decision-making and gain a competitive edge. Like sports data specialists, I am a sports fan and in this project I want to combine my love for football and data and use today's techniques to analyse and draw conclusions. I aim to identify the top-performing teams in set pieces and highlight the most influential players in regular gameplay.

## The data

To group NBA players, I use possesion percentatges in various play-types defined in the official web of the NBA. I use differents datasets. For clustering, I use 2 datasets, one for the 2018-2019 season and the other one for de 2019-2020 season. The 2019-2020 season dataset is in Kaggle and the 2018-2019 I find it in a Github repostiory mentioned in the end of this article. In total I have 583 players and 12 columns.

To analyse each new player-type and to suggets potential player acquisitions to teams, I use data extracted from Basketball Reference.

## Clustering
First of all, I read the data and clean it so that I can work comfortable. Our dataframe has 583 players with 11 variables. Apart from the name and the team of the players and the season, I have the frequency of each play-style. These play-styles are: 

- Isolation
- Pick & Roll Ball Handler
- Pick & Roll Roll Man
- Transition
- Post up
- Spot up
- Cut
- Handoff
  
Once I have the data cleaned, I can start to build our Kmeans model. 
I decide to use Kmeans but it's very important to choose wisely how many clusters to model. So my first step is to use the elbow method to find the optimal number of clusters in my data. Here is the result:

![Alt text](img/elbow_method.png)


Analysing the graph, I would declare that the optimal k is 4. However, I know nowadays there aren't only 4 types of offensive players, so I declare k=6.

Now, I fit the model with k=6 and add the new clusters to my data.

## Results

After reviewing how the model grouped my data, I can define the 6 different offensive player-type and see their characteristics in this HeatMap:

![Alt text](<img/HeatMap Clusters.png>)

The first cluster I name it **Spot Up Wing**. As I can see, these players usually spot up behind the arc and create in transition. Also, I can see that they operate more as handler than as a roll-man in the pick&rolls. **All Ofensive** players are defined by a high number of possesions in different play-styles. They usually create in transition, spot up behind the arc, they are the handlers in the pick&rolls and sometimes they play in isolation. Another cluster is **Rim Runners**. These players have an specific offensive style. They are always cutting and generate buckets through setting screens and rolling to the basket. Then, I have the **Post Up Big** that as the name says, they usually post up and operate as roll-man in the pick&rolls. The **On-ball Handler** as I can observe in the heat map are very defined by being the handlers in the pick&rolls but also sometimes they occupy exterior position to shoot, create in transition and are isolated. Finally, **Spot Up Big** are these big players that post up but also they can spot up behind the arc and make transitions.

Here is a list of 5 different players that are in each offensive type of players:

- All Ofensive: Stephen Curry, Paul George, Kevin Durant, Bradley Beal, Khris Middleton
- Spot Up Wing: Giannis Antetokounmpo, Julius Randle, Danilo Gallinari, Kevin Love, Lauri Markkanen	
- Rim Runners: Clint Capela, Domantas Sabonis, Myles Turner, Serge Ibaka, Rudy Gobert
- Post Up Big: Joel Embiid, Karl-Anthony Towns, Anthony Davis, Andre Drummond, Deandre Ayton
- On-ball Handler: James Harden, LeBron James, Devin Booker, Damian Lillard, Kyrie Irving
- Spot Up Big: Joe Harris, Robert Covington, Jaylen Brown, Trevor Ariza, Jae Crowder

![Alt text](img/players.PNG)

## Analysis

Let's see how these new players types are distributed:

![Alt text](<img/Barchart comparison.png>)

In this barchart I can see the 2019 and 2020 season behave similarly. In both season there are very few Post Up Bigs compared to the other types and additionally, All-Offensive, On-Ball Handler and Spot-Up Wing are the most dominant types in the game of basketball. Here I can see the modern era of basketball.

Now, I get the two Spot Up types to analyse the 3P% and 2P% of these players and see who are the leaders in these categories.

![Alt text](img/ScatterPlotSpotUp.png)

With this scatter plot I can observe that the points are very distributed independently of which type of Spot Up is. If I look deeper, I can see that in both characteristics the majority of the leaders are Spot Up Wings. That's quite foreseeable because these players are much more defined by spot up plays and usually their function is to be open and shoot. Despite all this, I must mention that the most complete player of these stats is a Spot Up Big, Meyers Leonard from the Portland Trail Blazers with 0.45 efficiency from three point line and almost 0.65 from the second line.

For the last part, I choose one player of one offensive type and I suggest 2 new signings and I compare these 2 players with the one I selected. This analysis could be applied to any player of any type.

For example, I choose Khris Middleton, an all-offensive player according to my clustering. Khris Middleton in 2019 had a salary of 13M/y. Now I compare him with 2 all-offensive players too: Bradley Beal (25.5M/y) and Jeremy Lamb (7.48M/y). *Salaries are taken from ESPN*

For the comparison, I decide to use radar plot so that I get some stats together and I can compare the players in each stat. The stats that I decide to use, with nothing in mind just that for me they are important stats for these types of players, are:

- PER: overall rating of a player's per-minute statistical production
- TS%: a measure of shooting efficiency that takes into account 2-point field goals, 3-point field goals and free throws
- AST%: An estimate of the percentage of teammate field goals a player assisted while they were on the floor
- USG%: An estimate of the percentage of team plays used by a player while they were on the floor
- BPM: A box score estimate of the points per 100 possessions a player contributed above a league-average player, translated to an average team
- eFG%: his statistic adjusts for the fact that a 3-point field goal is worth one more point than a 2-point field goal


![Alt text](img/RadarPlot.png)

So let's draw conclusions using this radar plot. As I can see, Bradley Beal (red line) is the most complete player between them being the best in the majority of the stats. But looking closer, if I observe Khris Middleton (blue line) and Jeremy Lamb (green line), Jeremy Lamb is better than Middleton in BPM and PER but basically, they are very similar except for the AST% that middleton seems to be in another league.
A team must take into account a lot more data to decide if it's viable to replace one player with another but with these radar plot I can conclude Jeremy Lamb could have been a reliable option if Milwaukee Bucks wanted to replace Khris Middleton back in 2019.

## Conclusions
In conclusion, in this project I applied K-means clustering successfully and I defined new offensive play-types based in data. After that, I analysed my clustering and made a few plots that helped to understand the modern era of basketball and to highlight different players that without the data we would not pay attention to at first glance, like Meyers Leonard.

Finally, I provided a practical application by suggesting potential player acquisitions to replace players with similar playing styles. This aspect contributes significantly to strategic decision-making for NBA teams looking to bolster their rosters with players who can seamlessly fit into existing systems.

This is my first project in Sports Analytics and I have enjoyed it and I hope to continue learning and putting into practice all the knowledge I am acquiring.

## Suggestions for improvement

In this project I used data from 2018 & 2019 about possesion percentatges in various play-types. To enhance the clustering analysis and achieve better differentiation among player clusters, I could consider incorporating additional data sources. Data like player physical attributes or stats of the game could provide a more comprehensive understanding of player profiles and playing styles. What's more, I could go deeper into the analysis and study more the differents defined play-types.


## Reference

https://www.nba.com/stats/players/transition NBA Stats

https://www.basketball-reference.com/ Basketball Reference

https://medium.com/playing-numbers/beyond-the-arch-introducing-a-new-way-to-understand-the-game-92c30b1a8599 by Brennan Ruby

https://towardsdatascience.com/redefining-nba-player-classifications-using-clustering-36a348fa54a8 Ahmed Jyad

## Contributors

Gabriel Gausachs