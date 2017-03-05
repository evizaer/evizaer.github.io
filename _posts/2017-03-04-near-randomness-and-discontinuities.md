---
published: true
---

In my article introducing [near and far randomness](http://nohidden.info/agency-and-randomness/), I talked in vague terms of the distance of randomness from the player's actions, and how randomness forces variation in the course of the game's events, sometimes at the cost of [agency](http://nohidden.info/agency/). Now, to further elaborate on the thought process of near and far randomness, I will elaborate on what makes certain cases of near randomness onerous, and through that develop ways to maintain the closeness of randomness to player action, but at the same time tame the damage done to agency.

# When Randomness Matters: Discontinuities

Players care much more about random results that cause certain numbers to cross certain boundaries. Even direct and seemingly close randomness can be effectively blunted through an understanding of when changes caused by randomness immediately matter and when they don't. Randomness denies agency most when its effects immediately generate a big response from the system.

Consider hit points in a typical Dungeons and Dragons-like combat system: The specific number of HP a character has doesn't matter much to the game's rules unless it crosses a certain critical threshold: 0. At that point the rules intervene in a profound way by severely curtailing the player's choices with that character. Yes, this is a weird way of putting "the character dies", but I want you to be thinking about the peculiar way that a number, usually representing some resource, doesn't mean much until it crosses a threshold, then it means *everything*. 

I call this a discontinuity. It's a point at which a small, incremental change in the amount of a resource causes an outsized effect after otherwise not meaning much.

Some discontinuities, like death, are forced by the rules, some merely open up new options to the player. In the same D&D-like game, the amount of gold coins a player has allows them to buy different items. We can see each item they could buy as a discontinuity in the value of gold pieces. If you want to buy a 5gp sword, the difference between 3 and 4 gp is meaningless, though the difference between 4 and 5gp is huge. But it only matters if a few other conditions are fulfilled: player has to be at a place where he can buy a sword, and the player has to volunteer to spend that money. There are, thus, a series of decisions and eventualities between the random event and the player actually buying the sword. This is in contrast to the automatic, rule-enforced action of dying at 0HP, which is universal (it has no conditions attached, except for some very rare cases) and involuntary.

The player's agency is damaged more when a difference decided by randomness crosses involuntary and unconditional boundaries. When an enemy dies, it matters a lot to the player, since that's the end of a threat to the player character's own life. If that threat hangs around one or more additional turns because of dice rolls, and those dice rolls happen at the last possible moment between the monster being alive and being dead, the player has had the causal chain of an event that really matters to them torn out of their hands. This is an acute loss of agency. When the player has to do 5 damage to kill an enemy and their weapon does 4 to 6 damage, nothing stands between the player and his valuable short-term objective except for the roll of the dice.

## Close dice rolls, far randomness.

To demonstrate how we can improve the use of randomness by purposefully avoiding discontinuities, let's take a look at randomized damage in that generic Dungeons and Dragons-inspired RPG mentioned above. The critical discontinuity in the act of dealing damage occurs when the opponent's life total is lower than the max damage of the weapon, but higher than its minimum damage. 

Since damage is determined by rolling dice, at what time the player manages to reduce the monster's HP to 0 is highly variable. Rolling a few 2s and 1s on six-sided dice over multiple turns can be the difference between the opponent being long dead and being very alive. That's a ton of near randomness. 

But if we make some alterations to this design, we can make that randomness less near without moving it to an earlier time and thus giving the player time to react to it. The crucial step is to stop thinking of damage numbers in terms of their absolute values, and instead think about them in terms of the variance they cause in the time it takes to kill an enemy with a typical HP total. 

Immediately this change of orientation produces some counter-intuitive results. Allowing weapons to do 0 damage seems pretty innocuous if you're only looking at absolute numbers. But if you look at it from the perspective of time-to-kill, it pushes the maximum value out to infinity! The player can sit there and has a non-zero chance of swinging at an opponent forever without killing it. That's way worse than if you had all attacks do a minimum of 1 damage--it's so much better to have combat be potentially of variable length but definitely end at some point.

Aside from making it obvious we have to get rid of 0 damage, we can use this new perspective to see two techniques to push randomness out:

* Make sure we only vary time-to-kill by relatively small amounts if it's a one-on-one fight. (It gets more complicated with multiple friends attacking an enemy and vice versa, but there are ways to handle that, too.) This means to keep damage numbers from varying by large percentages.

* Never let randomness account for the killing blow. If the player does 4 to 8 damage and the enemy has 6 HP left, have a rule that either says that the enemy will definitely die or that it will definitely live with a predictable amount of HP.

The net impact of these changes is that players will be able to predict when something is likely to die more accurately as it gets closer to dying. The design still allows for variation in when exactly something will die, but it doesn't submarine the player's agency by potentially randomly granting an enemy one, or many, more turns of life right before it *should* have died.

Through using this technique, we've moved what otherwise seems like close randomness into a place where it looks more like far randomness, even though we haven't changed when the dice are rolled much at all! It's all because we have an understanding of the discontinuities in some critical numbers in the game state.
