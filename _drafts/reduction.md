---
title: How Strategies are Born
---

In my article [on tension](link) I took a rule-focused look at what makes decisions interesting. In this article I will start with the player's mentality instead of rules. We can supplement the rules-focused model with a mentality-focused model to fill in some gaps.

In this article I'll present a thinking tool in the form of a model of how players might think of what move to choose next in a strategy game. The objective is to help you understand how to push your design towards more interesting decisions by considering the player's approach to weeding through their options to reach their goal.

To form a strategy--to plan future actions--you must do two things in some manner. 

* **Forward simulation** -- You forward-simulate to explore potential futures and compare these possible futures using some process of valuation. Forward-simulation encompasses both the process of imagining concrete game states one move at a time, as well as more loosely estimating where the game might be after some number of turns assuming you pursue some course of action outlined by some principles.
* **Relative valuation** -- a process through which you weigh possible futures against one another, eventually resulting in a single future you want to reach and the one move you do now to try to get to that future. 

When you strategize, you do both of these things at once. Though there are countless ways of doing forward simulation and valuation, both are necessary components of any decision-making technique.

## Forward Simulation

You can only mentally simulate so much. Strategy games overwhelm your mental faculties through the wealth of decisions they offer over time. You may have a better ability to perform mental spatial manipulations, while someone else may be able to store more numbers in their head at once, while a third person may be way better at piecing together hidden game state based on only the implications of others' play. 

As you get better at a game, you learn to chunk information better. This allows you to think further in the future and get stuck on fewer branches of the decision tree that are unlikely to bear fruit. 

The effectiveness of forward simulation is always closely tied to your ability to compare those futures and evaluate which is better. Your evaluative skills not only compare and eliminate possible futures, but tell you which moves might have futures worth simulating towards in the first place. A person with limitless mental capacity who can only tell when he has won the game but can't evaluate intermediate states accurately can only reliably win very simple games. Put him in front of Chess and he'll churn away in the early-game, exhausting the decision tree and himself in the process, without ever being able to make a single good move.

## Valuation and Reduction

Valuation is approximation in tough conditions.

As I outlined in my article on tension, you form strategies by fractally telescope subgoals from the game goal on down to a goal you can trivial achieve by performing a specific move this turn. Deciding which subgoals are valuable and worth pursuing is where valuation comes in. As long as you can assess if you've met a subgoal, you just need to figure out which is worth your time.

You can also imagine subgoals as metrics the player uses to judge his moves. Some of these in Chess are center control, piece development, and pawn structure integrity. The player needs to concoct a way of measuring the metrics against one another to choose one which will have precedence over the others. Since you can often make varying levels of progress towards and away from several different subgoals each turn (i.e. improving and reducing different metrics), you need to regularly navigate the conflicts between these subgoals and identify when it's beneficial to sacrifice one for the good of another.

Players improve the evaluation of sub-goals through a process I call "reduction." Through reduction we take several outcomes with diverse effects and compare them based on one or more common measures--there are many ways in which to measure a game state, so reducing the set of measurements we consider is a required step in boiling down multiple appealing moves into the one we'll actually do. Reduction is necessary because you can't compare actions without reducing their effects to some comparable measure. Reduction is at the root of skilled strategizing because through reduction you approximate what will give you the best chance of winning. Reduction is often nebulous, but it can sometimes be a very sharp process, like in comparing various resource conversion techniques in the interest of reaching a certain resource amount as fast as possible. 

## Creating gameplay to support multiple metrics

Localization of effect and hard effect boundaries lead to force allocation problems. Each region's strength becomes its own metric which is sensitive to opposition.

## Mechanical Irreducibility

It's easy to reduce direct numerical relationships. It's an equation-solving process that adults should be able to do.

Spatial relationships are harder because of localized effect. It becomes difficult to make sense of mathematical relationships that only cover a certain area of a space.

You can't reduce non-transitive mechanisms. RPS is irreducible by definition. 

## leftover stuff

The sub-goals are themselves creations of the player based on salient conditions, which they think will bring them much closer to winning if they achieve. Sub-goals can be simple--taking a bishop in Chess--or complex and more nebulous--like achieving control of the center in Chess.



(@Rewrite in light of above intro)
Designing a good strategy game is thus constructing an environment where it is difficult to perform this process of reduction. Players will always want to reduce valuation to a single measure which can be reliably derived for all possible actions. This represents a "reduction" of many different dimensions of state and situationality into an unconditional absolute measure, and the death of interesting decisions. Game systems should be resistant to such reductions. Non-transitive mechanics are one way of permanent resistance. Randomness is actually not one.

RPS resists reduction by axiomatically fixing payoffs along the only dimension of valuation.

Short-run prediction vs. clarity of valuation: You can't calculate a game out to its end, so you find a way to value intermediate states. You can get better at this valuation separately from your ability to calculate and predict play in the short-run.
