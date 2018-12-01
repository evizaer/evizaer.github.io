---
published: true
title: "Incentives and Intent: XCOM’s Creeping Forward Problem"
---

You can better design games when you can keep two clear and separate pictures in your head at once: what your game incentivizes the player to do, and what you want the player to do. Often designers only have a grasp on what they want the player to do so their playtesting consists of doing those things and making sure they work. Regardless of the clarity of the designer’s vision, the player does not have access to it and will follow the game’s incentive structure. Even relatively small misalignments between intent and design can cause the end result to look markedly different if not broken. For instance, an RTS with a slight imbalances in unit design will see players neglect most of the unit types available to them in favor of building the one imbalanced unit or its counter. 

Designers benefit from achieving a critical distance from their work and trying to re-learn their games so they might play in a way independent of their own preconceptions of how they intended the game to be played. This is no easy task, but practice analyzing the incentive structure of games where you don’t already know designer intent can equip you with the tools to achieve critical distance and analyze how incentives influence player behavior in your own game.

The basic process is this
1. Pick out a class of decision that feels off to you.
1. Write down the design elements that factor into that decision.
1. Check your list by putting yourself back into the same situation and re-making the decision based only on the factors you wrote down. See if there could be other viable options you could’ve chosen based on those factors. 
1. Add factors until your choice is the only one you can imagine taking given careful consideration of the factors you listed. (Also toy with removing factors if no instantiation of a factor can make you change your decision.)
1. Trace factors back to design elements and conduct thought experiments like “what would I do if X worked like Y instead of Z?” Start from the simplest changes that might fix the decision which feels off.

In this article I’m going to analyze a part of the incentive structure of XCOM 2012’s tactical combat. The goal is to learn why the optimal strategy when not engaged in firefights with aliens is to slowly creep your squad around the map, revealing a minimal number of tiles each turn. 

XCOM 2012’s combat system is otherwise dynamic and tightly-designed. It should encourage its players to fully embrace its complexity. The design should encourage the player to show aggression so that the player can get into interesting, dangerous situations more often and thus experience the full intellectual and emotional gamut the combat system can deliver.

In this article, I will analyze the incentive structure of tactical missions in XCOM 2012 to find the causes of boring and degenerate map exploration tactics, then talk about how XCOM 2 tried to improve on its predecessor’s design in this area. 

## The Rules

In XCOM, the player and enemies alternate turns in which all of their characters can act. the player can issue orders to her characters in any order, but each command is permanent. The player’s turn ends when all her characters have taken actions.

![Screenshot of XCOM2012](/images/xcom2012-1.PNG)
(Image taken from [Beaglerush's fantastic let's play](https://www.youtube.com/watch?v=T-cBJc38O_k&list=PLXctaw5JGF4LcidFVdkQMV1tc2DfC8x3D).)

The player can only see the tiles within line of sight (LoS) of her squad members at the moment. The majority of the map is shrouded in darkness. Hidden throughout the map are several groups of enemies (called “pods”) that move each turn. Hidden enemies do not move in predictable ways. Some missions also have a small number (or just one) pod that sits in a fixed place on the map, or patrols a very small area like the main room of a UFO. 

If the player doesn’t encounter enemies for a few turns the game gives the player a clear visual cue which tells her the general direction of a nearby pod. Aside from this, the player can only get hints to the position of hidden pods when flaws in the fog of war allow the player to see faint traces of aliens opening doors or breaking windows that are out of the squad’s line of sight.

The challenge in any mission comes from defeating the enemies on the map. At any given time enemies are either in an active state, where they’re fighting the player’s squad, or in an unactivated state, where they “wander” the parts of the map that the player cannot see. 
A player activates an entire pod when any member of that pod gains LoS on any member of the player’s squad. Since the player cannot activate less than one pod at a time, the pod represents a basic unit of danger in the mission.

The objective of a mission usually involves killing all enemies or reaching some location. EIther way, the player must move across the map into unknown territory to fulfill the objective. Each tile the player reveals may contain an enemy and thus activate a pod, even when the player is currently engaged with another pod.

Soldier and alien LoS is reciprocal. Once the player sees enemies, those enemies will activate. A notable exception is the “battle scanner” item, which a soldier can throw into the distance and gain temporary vision of enemies such that they won’t activate. Most of the time the player will activate enemies by moving one of her characters such that it gains vision of an enemy.

Dealing with one pod is manageable but can be tricky, dealing with two can be lethal, dealing with three is likely to cost the player multiple characters or wipe out her squad entirely. 

## The (Dis)incentives

The costs of attempting the unnecessarily dangerous in XCOM are high. Characters that die in missions are gone forever, and injured characters may be unavailable for several missions. 

The design of the strategic layer of XCOM steadily increases the challenge level of tactical missions with minimal regard for the player’s success or failure. The game offers a hard-pressed player no breaks and often drives her into a campaign-ending death spiral through the cumulative loss of resources over several missions. Death-spirals take this shape: the player’s most powerful characters get injured, meaning inferior characters go on missions and have a higher likelihood of also suffering injury or death. Since the top character is injured, she is not gaining experience and advancing. Weaker characters go on missions that are above their means, so it’s more difficult for them to survive so they can grow in power. On the whole, the player with less skill falls progressively further and further behind the mounting difficulty, defeat feeding on defeat.

The game makes it abundantly clear to the player thematically and mechanically that she shouldn’t want to take injuries or have characters die for any reason if it can be avoided. The simplest way to avoid such pitfalls is for the player to engage as few enemies as possible and engage them one at a time.

The mechanics shape combat into a trial of risk minimization techniques. The player will rely on deterministic ways of dealing damage, like grenades and rockets, and seek the safest possible engagements by crawling forward and fighting as few aliens at a time as the game will let her.

Incentives combine to constrain the player into playing in a way that reveals as few tiles as possible on their turn and ensures that multiple squad members’ turns are available to deal with pods that may activate. The resulting play is a deliberate crawl across the map. The player’s first move is to advance her forward-most character, then follow with the rest of the squad such that no move but the first reveals tiles. Most of the player’s commands are revealing nothing, and most of the player’s time is spent waiting between turns or watching character-running animations.

What would the player gain by completing missions quickly? The game’s systems provide no incentive to do this, but a player may find it boring to play as conservatively as the game allows. A knowledgeable player trying to play her best is forced into the awkward situation of having to choose between spending a lot of time playing in a boring but correct way, or spending less time playing in a more fun way but one that lowers their chances of success for no in-game benefit.

This fun-for-effectiveness trade-off hurts the design. The design punishes the player for engaging the most stimulating and interesting kinds of dangerous combat situations. The design gives the player no reason to seek challenge, so the smart player studiously avoids it.

In the next article I will look at the way XCOM2 and the Enemy Within expansion for XCOM2012 try to address this problem.
