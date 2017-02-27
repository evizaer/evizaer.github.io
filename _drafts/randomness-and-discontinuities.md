---
published: false
---

Players and designers spend an incredible amount of time and effort grappling with randomness' role in strategy games. In this article I'll develop a model for understanding the impact of randomness on agency, which will hopefully clarify the use of randomness as a design tool.

## The Context

Strategy games are about the player expressing skill in decision-making. Strategy games give the player [agency](http://nohidden.info/agency) in trying to achieve some pre-defined goal under varied conditions. What the player chooses to do must have an important role in determining if they achieve their goal.

The player expresses skill in how they react to whatever happens in the game, in terms of how much they can use events to get to their goal. It's critically important for designers to always be thinking about how the player could've done something differently with the knowledge she had when making a certain decision. Trace the causal links between the player's success or failure, the information they had, and their actions. Is there a clear causal link, or did the result come out of nowhere? Did a monster spawn so close to the player's avatar that the player could do nothing but put up meager resistance before being slaughtered? Could the XCOM player have known that they will miss three attacks in a row and that would give their enemies time to kill one of the player's squad members? Was the player locked into a losing path and all the good decisions they made after a certain point were futile, even though they had no real way to know?

## Randomness as a Design Tool

We can think of a strategy game as a big list of possible things that can happen which is determined by the rules of the game and the participation of the player. The player is interested in finding out what's going to happen, and their uncertainty about the result combined with their power to influence the result pushes them on to play more.

In a single-player game with no randomness, the player is the sole decider of what happens and the game acts as an impartial judge that figures out the immediate results of the player's input then waits for more input. In the player's pursuit of the goal, their job is to filter through all the stuff that can happen so they can find a path that will lead them to achieve their goal. This can get boring, because the player will filter out most of the variety of the game in their effort to achieve the goal, since way more can happen than the player *wants* to happen. This hurts variety a lot, making the game become monotonous and boring way too quickly. There may be ways to get around this by designing systems with many complex emergent properties, but it doesn't seem like this approach has seen any practical use. The standard technique is to use randomness. The designer can deploy randomness as a way to lessen the player's filtering power. Randomness can force new events into the player's consideration by virtue of the player simply not being able to control them. This is how designers use randomness to achieve more variety.

## Near and Far

Since we care about just how much and in what ways the player can react to random events, we need to pay close attention to How much game-metered time elapses between when the player becomes aware of the result of a randomly-determined event and when the player is directly affected by it. I use the concepts of "closeness", or "near" and "far" randomness to capture this idea.

An enemy randomly spawned within range to attack the player before the player can act is an example of very close randomness. An enemy spawned several turns of movement away from attacking the player is an example of randomness that's more far than near. The real consideration here isn't actual physical distance on the game's map, but a measure of time. Near randomness is often *too close* in terms of map distance--but that also makes it *too soon* in terms of time.

Near randomness hurts agency but aids variety. But if we push randomness further away from the player's inputs, we provide variety without compromising agency in a significant way. The randomness then makes the player play differently through providing new stimuli for the player to react to. This expands the number of possible combinations of events the player can encounter while maintaining the player's agency by avoiding salient, powerful near rendomness.

(If you are familiar with the terms "input randomness" and "output randomness", you have just seen a derivation of their meaning. Input randomness is far, output randomness is near.)

(@Idea far randomness is diffuse. THink of randomness like light. You want it to be cast across the game to light up plenty of new events, you don't want it burning a hole in any one particular place.)

## A Catch

Far randomness is not a cure-all. Since designers do not have solid and implementable abstract models of decision difficulty and player skill, there is no way to verify that the difficulty variation caused by the far randomness is even and fair. To fairly assess the player's skill, the player must play through multiple sceanrios that test them in different ways and through this multiple-sampling approach of measuring skill the peaks and valleys of difficulty are averaged out. Far randomness works best when there is a relatively short standard unit of play, and the game can assess the player's skill by aggregating the results of all plays.

## Deceptive Distance

* We can move randomness that first appears near into something further out by assessing discontinuity-crossing and eschewing allowing randomness to cross discontinuities.

* Map generation in DCSS. Multiple stairways down is good because going down is near randomness (quick exposure to nearby enemies that could be very dangerous). Blind corners make map gen randomness more near than far. DIscontinuities in information reveal.

## Discontinuities

There is one key concept you need to master in order to gain a significantly better understanding of how to effectively use randomness to achieve variety in game design at minimal cost to agency. You need to analyze the effects of randomness through identifying discontinuous results.

* (@ Maybe don't do this here) Nature. How big is the effect of randomness? Does randomness choose between values along one dimension, or does it have a composite effect? Does randomness choose what a player can do, or does the player choose how to employ randomness?

## What is discontinuity?

Consider hit points in a typical Dungeons and Dragons-like combat system: The specific number of HP a character has doesn't matter much to the game's rules (@Comment strategic evaluation of players?) unless it crosses a certain critical threshold: 0. At that point the rules intervene in a profound way by severely curtailing the player's choices with that character. Yes, this is a weird way of putting "the character dies", but I want you to be thinking about the peculiar way in games that a number, usuaally representing some resource, doesn't mean much until it crosses a threshold, then it means *everything*.

I call this a discontinuity. It's a point at which a small, incremental change in the amount of a resource causes an outsized effect after otherwise not meaning much.


# from a DFF post.

But I think there's a further distinction to make here: quantitative results can have continuous or discontinuous effects. By this I mean the difference between killing something and just lowering its HP in a game where HP has no other effect. The valuation function for the outcomes of this randomness have an enormous discontinuity at the point which damage = remaining HP. This big, immediate jump in value seems far worse than a random damage result that changes the mean time till killing an enemy from 3 turns to 4. The distance between the randomness changing the game state and the discontinuous change in game state value is the crucial element. You want the randomness to feed into several turns of decision-making, in which its effects can be mitigated, instead of making the big jump in board value suddenly and wholly because of a randomly generated number. The big jump definitely requires a reaction from the player, but only after the fact since it's over so quickly (perhaps without any reaction possible before the big jump); the agency the player has in the result is way lower.
