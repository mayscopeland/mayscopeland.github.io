---
layout: post
title:  "How the Price Guide Works"
---
*(The material in this article was originally posted as a series of four blog posts from December 2008 to January 2009 to introduce my fantasy value calculator (The Price Guide) on my original Last Player Picked site. Since that site no longer exists, I've copied the series into a single article here.)*

I’ve stated that I believe the key to making the Price Guide the best possible tool for fantasy player valuation is to be transparent with how it works. By disclosing exactly what is going on, I hope that the community will be able to point out any flaws I have overlooked and provide insight into ways to improve.

With that in mind, I’m going to take a few posts to explain the methodology the Price Guide is using. A good deal of it is drawn from [discussions elsewhere](http://www.insidethebook.com/ee/index.php/site/comments/the_worth_of_sb_hr_and_all_other_categories_in_fantasy_baseball/), but there are some unique aspects as well. (I also realize this is probably not terribly interesting stuff, so I figure that it is good to discuss it now while I’m basically just talking to myself.)

# Part I: Z-Scores
All of the systems for valuing players are based on finding the worth of the fantasy stats in relation to each other. All else being equal, is a player who hits 30 HR worth more than a player who steals 30 bases? How do those two relate to a player with 30 saves?

Comparing those players is not as simple as saying 30 = 30. Saves are more scarce than homeruns, and fantasy teams typically end up with far fewer saves than homeruns. Because they are more rare, each save is more valuable than each homerun. What we need to find out is exactly **how much** more valuable each save is.

To do this, we need to be able to put these various categories onto a single scale. This is actually a common problem in statistics, and the way it is solved is with z-scores. Z-scores will work perfectly for fantasy as well.

To compute the z-scores for each player’s stats, we want to subtract the stats of the average player and divide by the standard deviation for the pool of drafted players. That might sound complicated, but it is easy to do if you have a spreadsheet (and even easier with the Price Guide).

As an example, let’s generate values for a shallow, mixed league that uses the default Yahoo settings. In this league, there are 12 teams that each draft 9 hitters, meaning that a total of 108 hitters will be drafted for starting lineups.

Using the Marcel projections, then, the average stats for those 108 players will be:*

BA: 0.2840
R: 76.8
RBI: 75.7
HR: 19.5
SB: 10.5

## Some Extra Work for Rate Stats
However, we need to do some extra work to find the z-scores for BA. If a player has 2 AB all year and gets 1 hit, they’ll have .500 BA. A player who has 600 AB and manages 200 hits will have a lower batting average (.333), but this player makes a greater positive contribution to a fantasy team’s BA than the first.

What we need to do is convert BA from a rate stat to a counting stat. To do that, we ask, “How many more hits would this player get than the average player, given the same number of AB?” We know that the average player will bat .284, so the formula for each player is:

xH = H – (AB * .284)

Consider the player above with 1 hit and 2 AB. The average player, given 2 AB will get 0.568 hits (2 * .284). Our sample player got 1 hit, or 0.432 above average (1 – 0.568). The formula explains how this works out:

xH = 1 – (2 * .284) = 0.432

For the other player, the formula yields:

xH = 200 – (600 * .284) = 29.6

That fits with what we expect-–a player who bats .333 throughout the season is much more valuable than a player who hits .500 in a very small sample.

Having computed xH for each player, we will use the average of xH instead of the average BA (.284). Our new averages are:

xH: 0
R: 76.8
RBI: 75.7
HR: 19.5
SB: 10.5

The standard deviations for each category:

xH: 8.0
R: 11.6
RBI: 14.4
HR: 6.6
SB: 9.9

## Computing Z-Scores
With the averages and standard deviations in hand, it is now possible to compute z-scores. Let’s use David Wright as an example, who Marcel projects for 96 R, 101 RBI, 26 HR, 19 SB, 169 H, and 549 AB.

xH = 169 – (549 * .284) = 13.1

mH = (13.1 + 0) / 8.0 = 1.6
mR = (96 – 76.8) / 11.6 = 1.7
mRBI = (101 – 75.7) / 14.4 = 1.8
mHR = (26 – 19.5) / 6.6 = 1.0
mSB = (19 – 10.5) / 9.9 = 0.9
Total = 1.6 + 1.7 + 1.8 + 1.0 + 0.9 = 7.0

Without any context, it’s not clear if those are good values or not. But if you do the same process for all the players, you’ll find that Wright has a very high value in all five categories. In fact, he ends up being the highest valued player in this league.

Also notice that, if you plug in the stats of the theoretically average player, his value in each category will be 0. So any player with a positive value for a category is above average in that category; any player with a negative value is below average.

We now have a preliminary value for each player, but our work’s not done yet. Before we can generate dollar values, these values need to be adjusted to take into account the replacement level at each position. That will be the subject of Part II.

\**You may have noticed that I left out one crucial step here: How did we figure out who the best 108 players were before we generated values? The Price Guide handles this by going through the entire valuation process multiple times until it arrives at the optimal draft pool. This iterative approach is a topic I’ll tackle later on in this series.*

# Part II: Positional Adjustments
In our previous example, we had a standard Yahoo setup with 12 teams and 9 hitters per team, for 108 total players drafted. In this league, there will be 12 players drafted at each position.

Notice that, in an auction, the last catcher drafted will go for $1, and the last 1B will also go for $1. This is true even though the last 1B is expected to produce much better stats than the last C. And that’s the key point: Despite the variance in expected production, the last players drafted at each position have the exact same value.

With this in mind, we want to adjust our values so that the last players picked at each position have equal values. In our sample league, the 12th best SS according to Marcel is Ryan Theriot, with a value of -2.97. The 12th best catcher is much worse–Chris Iannetta at -6.26. So for all of the SS, then, we will add 2.97 (i.e. subtract -2.97). For catchers we will add 6.26.

Now Theriot and Iannetta have the same value (0), and there are exactly 11 SS and 11 C with positive values. When this adjustment is done for all of the players, there will be exactly 108 players that have a value of zero or greater.

Notice just how huge of a bump this is for catchers. Before, Mauer, Martin, and McCann looked like 4th and 5th round selections (or $15-20 players). Now they land in the top of the 2nd round–worth upwards up $35.

The change is less dramatic for the other positions. Typically, middle infielders will get a small increase of $1 or $2; corner infielders (and often outfielders) will see a slight drop.

## Flex Positions
There are a couple of complications when trying to find replacement levels. The first is dealing with “flex” positions like utility/DH, corner-infield, and middle-infield. To handle these, the Price Guide first marks all of the players that are above the replacement level at each of the regular positions. In our sample league, it marks 12 players at each of the primary positions, 96 in all.

Since our sample league uses a DH, the Price Guide finds the top 12 unmarked players and sets the DH replacement level at the 12th. David Ortiz is the top unmarked player, followed by Jim Thome. The remaining 10 are the best of the rest, typically 1B, OF, and 3B. For each player that is counted as a DH, that player’s value is used as the new replacement level for his primary position.

So the previous replacement level for 1B was -0.71, the value of James Loney as the 12th best 1B. But with the DH position, it turns out that 1B like Joey Votto, Conor Jackson, and Adam LaRoche are also worth drafting. The new replacement level for 1B drops to -2.07, which is LaRoche’s value as the 15th best 1B.

## Multi-Position Eligibility
The second issue is handling players who are eligible at more than one position. Their value should be based on the most valuable position they are eligible at. However, if I move all of the multi-positional players to the most valuable position, it makes that position less valuable (because there is more talent available). Their old positions become more valuable, because we have fewer quality players to choose from.

There’s a possibility of getting stuck moving players back and forth between positions trying to find the most valuable position. Because of this, the Price Guide assumes the positions are ranked as follows (from greatest to least):

C
SS
2B
3B
CF
LF
RF
OF
1B
MI
CI
Util

That works for most leagues, but there may be situations where it is less than optimal. I haven’t discovered a better way to handle it programmatically, and it shouldn’t make much difference most of the time.

For a straight draft, once we have done the positional adjustments, we’re done! The players should all be ranked correctly. For an auction, however, the final step is converting our adjusted values into dollar values. That shouldn’t take long and will be covered in Part III.

# Part III: Dollar Values
The final step in figuring out player values is to convert our values into dollar amounts. The example we’ve been working with is a standard Yahoo league–12 teams, 5×5, 9 hitters and 7 pitchers. For this last step, let’s also assume that each of the 12 teams has $260 to spend on starters at the auction, with a $1 minimum bid.

Since everyone has to spend at least $1 per position, we know there will be $16 per team that is essentially reserved from bidding. That gives everyone $244 marginal dollars to work with, and the league as a whole $2928 to spend.

We also know that if we add up the value of all of the “draftable” players (i.e. those with a positive value after the positional adjustment) we have 529 units of value that will be bought at the draft. Knowing the total amount of money and the total amount of value, we can set up this formula to determine the money each player is worth:

$ = (player value / 529) * $2928 + $1

Dividing the player’s value by 529 will give us a percentage of the total value that that player represents. We multiply that percentage by the total marginal money at the auction to get that player’s percent of the money. The $1 added on the end is what we reserved as the minimum bid for each player.

In Part I, we calculated David Wright’s value in this league at about 7 units. After the postional adjustment in Part II, he ended up at about 9.6. Plugging that value into our formula:

$ = (9.6 / 529) * $2928 + $1 = $54

The results are what we would expect for our last players picked, too. In this league Jorge Cantu ended up as the replacement level 3B, worth 0:

$ = (0 / 529) * $2928 + $1 = $1

So the last player goes for $1, which conforms to what actually happens at the draft.

## The 70/30 Split
It’s an accepted rule of thumb in fantasy that about 70% of money should be allocated for hitting, and the remaining 30% saved for pitchers. Why didn’t I split the money up that way when I determined the dollar values above? The short answer is that I didn’t have to.

If you use this method to calculate dollar values for all of the players, you will find that 64% of the money ends up allocated to hitters, and the remaining 36% goes to pitchers. For a traditional roto league with 14 hitters and 9 pitchers (AL-only, NL-only, or mixed), the split winds up right at 70/30. The Price Guide displays at the top of the results how the money ends up being allocated between hitters and pitchers, and it is usually pretty close to what you would expect.

So don’t worry about the various explanations as to why two-thirds of the auction money goes to hitters; the split is just a function of how players are valued. The numbers confirm what fantasy players already knew, even if they haven’t understood why.

That sums up most of what goes into the Price Guide. The only thing left is something I hinted at in Part I, when I mentioned using the best 108 hitters. In Part IV, we’ll look at how we managed to come up with the top 108 hitters, even before we ranked the players.

# Part IV: Iterations
In Part I on this series, I explained how the first step of creating fantasy baseball values was finding z-scores based on the top 108 players (for our example 12 team league with 9 hitters per team). I also hinted how this presents a bit of a catch-22: We need to know who the top players are before we can rank them. But we need to rank them before we can determine the top players.

The Price Guide’s solution is to perform the valuations iteratively. Each time it processes, it feeds the top players from the previous iteration into the current one. It keeps going through that process until the results from a previous run are identical to the current run. At that point it has found the optimal player pool.

That means that the first time it runs, it assumes that the first 108 players it comes across must be the top players, regardless of how the list is initially sorted. If the list of players is in alphabetical order, the Price Guide will plug in guys like Reggie Abercrombie and (the humorously named) Andy Abad to come up with z-scores.

Even using these guys, the cream rises quickly to the top. Think of it this way: If you’re in a league where Andy Abad gets drafted in the first round, it still makes tons of sense for you to grab Pujols. In fact, Pujols looks even more valuable in this league, because the competition is even further below him than usual.

So after one iteration, the rankings already look decent. The first round players are mostly ranked somewhere in the first round, although at prices that are too high. Things start to drift a little bit after that, but we are definitely a lot closer than at the start.

The second time through, the extreme values it gave to the top tier players are toned down a bit, and the rankings look like something you could bring to a draft without embarrassment. Each successive valuation after that is really just tweaking the draft pool–moving guys up or down a couple of slots, balancing speed and power, switching around some of the bottom of the barrel players. Within 3 to 10 iterations, it has settled on the optimal draft pool.

Anyway, that pretty well sums up the methodology I’m using to come up with fantasy dollar values. Looking back at the posts, I realize that this isn’t the most interesting subject to discuss. However, my purpose for this series is to provide some reference material–not necessarily enjoyable reading. So consider this series as Appendix A sitting somewhere near the back of the Last Player Picked site.

Of course, if you managed to wade through all four parts of this explanation and have any questions or comments, feel free to let me know.