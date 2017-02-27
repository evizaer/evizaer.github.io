---
published: true
---

Players and designers spend an incredible amount of time and effort grappling with randomness' role in strategy games. In this article I'll develop a model for understanding the impact of randomness on agency, which will hopefully clarify the use of randomness as a design tool.

## The Context

Strategy games are about the player expressing skill in decision-making. Strategy games give the player [agency](http://nohidden.info/agency) in trying to achieve some pre-defined goal under varied conditions. What the player chooses to do must have an important role in determining if they achieve their goal.

The player expresses skill in how they react to whatever happens in the game, in terms of how much they can use events to get to their goal. It's critically important for designers to always be thinking about how the player could've done something differently with the knowledge she had when making a certain decision. Trace the causal links between the player's success or failure, the information they had, and their actions. Is there a clear causal link, or did the result come out of nowhere? Did a monster spawn so close to the player's avatar that the player could do nothing but put up meager resistance before being slaughtered? Could the XCOM player have known that they will miss three attacks in a row and that would give their enemies time to kill one of the player's squad members? Was the player locked into a losing path and all the good decisions they made after a certain point were futile, even though they had no real way to know?

## Randomness as a Design Tool

We can think of a strategy game as a big list of possible things that can happen which is determined by the rules of the game and the participation of the player. The player is interested in finding out what's going to happen, and their uncertainty about the result combined with their power to influence the result pushes them on to play more.

In a single-player game with no randomness, the player is the sole decider of what happens and the game acts as an impartial judge that figures out the immediate results of the player's input then waits for more input. In the player's pursuit of the goal, their job is to filter through all the stuff that can happen so they can find a path that will lead them to achieve their goal. This can get boring, because the player will filter out most of the variety of the game in their effort to achieve the goal, since the game allows way more to happen than the player *wants* to happen. This hurts variety a lot, making the game become monotonous and boring way too quickly. There may be ways to get around this by designing systems with many complex emergent properties, but it doesn't seem like this approach has seen any practical use. The standard technique is to use randomness. The designer can deploy randomness as a way to lessen the player's filtering power. Randomness can force new events into the player's consideration by virtue of the player simply not being able to control them. This is how designers use randomness to achieve more variety.

## Near and Far

Since we care about just how much and in what ways the player can react to random events, we need to pay close attention to How much game-metered time elapses between when the player becomes aware of the result of a randomly-determined event and when the player is directly affected by it. I use the concepts of "closeness", or "near" and "far" randomness to capture this idea.

An enemy randomly spawned within range to attack the player before the player can act is an example of very close randomness. An enemy spawned within sight of the player but several turns of movement away from attacking the player is an example of randomness that's more far than near. The real consideration here isn't actual physical distance on the game's map, but a measure of time the event spends in the player's awareness. Near randomness is often *too close* in terms of map distance--but that also makes it *too soon* in terms of time.

Near randomness hurts agency but aids variety by forcing potentially large changes to the game state that the player can't do anything to mitigate or filter out. But if we push randomness further away from the player's inputs, we provide variety without compromising agency in any significant way. The randomness then makes the player play differently through providing new stimuli for the player to react to. This expands the number of possible combinations of events the player can encounter while maintaining the player's agency by avoiding salient, powerful near rendomness.

You can think of randomness like a powerful light. If you put it right next to your eye, it blinds you. You have lit up your surroundings but you've rendered it pointless since you now can't see. Only when you put the light an appropriate distance away does it illuminate your surroundings in a way you can actually use.

If you are familiar with the terms "input randomness" and "output randomness", you have just seen a derivation of their meaning. Input randomness is far, output randomness is near. But note that this turn's output randomness can be seen as next turns input randomness--yet in the near vs. far model this is not the case. This turn's near randomness did its damage to agency, and the only purpose it serves is to force variation in events. Near randomness never "turns into" far randomness as you play a game, or vice versa. Nearness is a property of when the randomness becomes a consideration for the player. In contrast, input randomenss is about if or when the random event becomes a consideration in the player's strategy.

## A Catch

Far randomness is not a cure-all. Since designers do not have solid and implementable abstract models of decision difficulty and player skill, there is no way to verify that the difficulty variation caused by the far randomness is even and fair. To fairly assess the player's skill, the player must play through multiple sceanrios that test them in different ways and through this multiple-sampling approach of measuring skill the peaks and valleys of difficulty are averaged out. Far randomness works best when there is a relatively short standard unit of play, and the game can assess the player's skill by aggregating the results of all plays.

## Conclusion

We can think of randomness in terms of how close it is to the player. Since players express skill by reacting to events in ways that draw them closer to their goal, giving the player plenty of room to maneuver around random events allows us to add a lot of variety to designs without it costing much agency.

