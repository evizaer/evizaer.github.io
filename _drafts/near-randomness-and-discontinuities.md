---
published: false
---

## Discontinuities

Near and far randomness is not just about the position of the randomness in relation to the player's actions. This is because we care much more about random results that cross certain numerical boundaries. Even direct and seemingly close randomness can be effectively blunted through an understanding of when changes caused by randomness immediately matter and when they don't.

Consider hit points in a typical Dungeons and Dragons-like combat system: The specific number of HP a character has doesn't matter much to the game's rules unless it crosses a certain critical threshold: 0. At that point the rules intervene in a profound way by severely curtailing the player's choices with that character. Yes, this is a weird way of putting "the character dies", but I want you to be thinking about the peculiar way in games that a number, usuaally representing some resource, doesn't mean much until it crosses a threshold, then it means *everything*. 

I call this a discontinuity. It's a point at which a small, incremental change in the amount of a resource causes an outsized effect after otherwise not meaning much.

To demonstrate how we can improve the use of randomness by purposefully avoiding discontinuities, let's take a look at randomized damage in a game similar to the generic Dungeons and Dragons-inspired RPG mentioned above. When the player does damage to an enemy, the player is aiming to reduce the enemy's HP to 0 and remove it from battle. Damage is determined by rolling dice. At what time the player manages to reduce the monster's HP to 0 is usually highly variable because of the nature of diec rolls. Rolling a few 2s and 1s on six-sided dice over multiple turns can be the difference between killing an opponent in four turns, or twenty turns on average. That's a ton of near randomness. 

But if we make some alterations to this design, we can make that randomness less near without moving it to an earlier time and thus giving the player time to react to it. The crucial step is not thinking of damage numbers in terms of their absolute values, but instead in terms of the variance they cause in time-to-kill an enemy with a typical HP total. We can use two techniques to push randomness out:

* Make sure we only vary time-to-kill by relatively small amounts if it's a one-on-one fight. (It gets more complicated with multiple friends attacking an enemy and vice versa, but there are ways to handle that, too.)

* 


* Map generation in DCSS. Multiple stairways down is good because going down is near randomness (quick exposure to nearby enemies that could be very dangerous). Blind corners make map gen randomness more near than far. DIscontinuities in information reveal.


There is one key concept you need to master in order to gain a significantly better understanding of how to effectively use randomness to achieve variety in game design at minimal cost to agency. You need to analyze the effects of randomness through identifying discontinuous results.

* (@ Maybe don't do this here) Nature. How big is the effect of randomness? Does randomness choose between values along one dimension, or does it have a composite effect? Does randomness choose what a player can do, or does the player choose how to employ randomness?

## What is discontinuity?



# from a DFF post.

But I think there's a further distinction to make here: quantitative results can have continuous or discontinuous effects. By this I mean the difference between killing something and just lowering its HP in a game where HP has no other effect. The valuation function for the outcomes of this randomness have an enormous discontinuity at the point which damage = remaining HP. This big, immediate jump in value seems far worse than a random damage result that changes the mean time till killing an enemy from 3 turns to 4. The distance between the randomness changing the game state and the discontinuous change in game state value is the crucial element. You want the randomness to feed into several turns of decision-making, in which its effects can be mitigated, instead of making the big jump in board value suddenly and wholly because of a randomly generated number. The big jump definitely requires a reaction from the player, but only after the fact since it's over so quickly (perhaps without any reaction possible before the big jump); the agency the player has in the result is way lower.
