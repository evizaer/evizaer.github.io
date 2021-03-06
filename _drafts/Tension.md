
Sid Meier's famous quote that "games are a series of interesting decisions" rests at the core of how many designers understand their craft. But we seldom examine what makes decisions interesting. Intuition can take us pretty far, since we all have plenty of experience with tough choices we've had to make throughout our lives, in games and out. But the structure of these choices, and how to design such choices in a controlled environment like a game, is seldom discussed in much detail. The three pieces of media that have tried to tackle this problem in games design are [Jon Schafer on what makes decisions interesting.](1), 
[Ian Schreiber's tips on decision-making](2), and
[Sid Meier's GDC Talk on Interesting Decisions](3) ([Leigh Alexander's summary](4)). I find all of these to be vague and unsatisfying. This article is my attempt to build up a theoretical groundwork for interesting decisions in strategy game design.

## Narrowing the Scope

For the purposes of this article, I will constrain "interesting decisions" to be goal-directed decisions made from a systemic perspective. I'll pass over some other putative types of interesting decisions, like cosmetic character customization, in the interest of having a clearly circumscribed area for discussion.

A critical part of interesting decisions I will not go into in this article is that of relevance to the player in a broader sense than systemic concerns allow. Few players are interested in making decisions about things if the only reason they have to make decisions about them is that a game is telling them so. We're interested in that which is personally relevant to us, and for many players that relevance is predicated on thematic choices that may have nothing to do with the system. Winnie the Pooh strategy games will turn off many potential players based on nothing more than that the player sees a child-oriented theme and assumes the game isn't relevant to them. This article will not discuss how to put decisions into the right cultural context to make them accessible and meaningful to players more broadly.

## Trade-offs: the Starting Point

Meier, Schreiber, Schafer agree that trade-offs make interesting decisions possible. I'm left with a lot of questions, though. What makes a trade-off? How can we look at a system without playing it and see where trade-offs occur? Are some trade-offs better than others for creating interesting decisions?

Trade-offs are an emergent property of decisions which arise from conflicts in incentives. When the player can't do everything he wants to do in a given span of time, a trade-off pops into existence: progress towards one desired outcome comes at the expense to some amount of progress towards another.

To better articulate the causes of trade-offs, I say that some game rules are *in tension* with one another. They vie for the player's attention as he tries to decide what to do next and in so doing provide the raw materials for strategy: if he hopes to win, the player has to piece together some coherent plan to take advantage of the natural synergies between rules and diminish or eliminate forces that get between him and the game's overarching goal.

To understand this in more detail, we must explore goals and sub-goals.

## First: Goal Structure

All incentives flow from the structure of sub-goals formed by the interaction between the game's goal, play environment, and available player actions. Any discussion of the tensions between game rules must start with a sub-goal analysis. To do this analysis, start with the game's goal and work backward to the game's starting condition, one step at a time, making reference to player actions and game concepts where possible.

Here's a goal analysis for Company of Heroes' adversarial multiplayer:
1. The game's goal is to reach 500 Victory Points before your opponent does.
1. To reach 500 VPs, you must control more Victory Locations at a tick than your opponent.
1. To control VLs, you must capture it and prevent your opponent from capturing it.
1. To capture a VL, you must have at least one unit close enough to it for a number of seconds.
1. To have a unit close to a VL, you have to move units to it and fight enemies who might stand in your way.
1. To move units you must have units to move.
1. You acquire units by building them at certain buildings.
1. You have to build buildings which permit you to build units.
1. You build buildings using your starting resources and engineers.

Resource acquisition and the game's economy is actually a parallel goal structure built into those last three steps.

1. To build units, you must have sufficient resources, buildings, and technologies.
1. To build buildings and research technologies, you must spend resources.
1. To acquire resources you must control capture points of different types.
1. You control capture points the same way as you control VLs.

I could go further and do a similar analysis for what it means to control space. This analysis involves talking about the counterplay between units. I will leave it as an exercise to the reader in the interest of brevity.

This analysis provides a high-level overview of what the player is incentivized to do in their pursuit of victory. Tensions arise when there are multiple ways to reach these sub-goals, where multiple concrete sub-goals vie for attention (e.g. should I try to capture the north or south VL?), or where progress towards one sub-goal can be traded for progress towards another.  A goal analysis doesn't show you where interesting decisions happen or why, but it reveals the superstructure which gives interesting decisions room to happen.

Now that we've got an analytical tool to help us find the sub-goals, we need to be able to combine that with an analysis of player actions to see how those actions create tensions in pursuit of the sub-goals. 

## Player actions

Tension occurs as a product of multiple appealing actions the player can take. These are the verbs players use to interact with the game. They are always parameterized further. E.g. to move a unit, a unit and a destination must be specified; to attack, at least an attacker and defender must be specified. 

Player actions have a few properties which exhaustively define them:

* **Payouts** -- some combination of resource or condition changes that happen once the player takes the action. (Ex. The payout for moving your piece into an enemy piece in chess is that the enemy piece is removed from the board. The payout for building a Barracks in Star Craft is that you can now build Marines.)
* **Costs** -- some combination of resources or constraining environmental changes that must happen in order for the action to happen. If you can't pay the costs, you can't take the action. (Ex. The cost of a Marine in Star Craft is 100 minerals, 1 supply, and a certain build time at a specific barracks.)
* **Conditions** -- what the details of the environment must be for the player to be able to choose the action. Conditions are like costs except they aren't "paid". The objects of conditions are not changed by taking the action. (Ex. You can't build a marine unless you already have a Barracks built.)

Payouts, costs, and conditions do not need to all be expressed as conjunctions of constants, like "pay 2 stone to build a wall segment". These properties can also be expressed as functions of one another, as in "If x enemies died last turn, deal x damage to an enemy where x is the number of red mana you pay."

## Components of Tension

Rules (player actions and environmental rules alike) come into tension with one another as a result of three properties interacting to create clashing incentives: exclusivity, situationality, and indirectness.

* **Indirectness** -- it must involve choosing between actions which indirectly move the player towards the game goal, thus obscuring their value. Without indirectness, the player can easily value each choice and choose that which has the highest value. 
* **Exclusivity** -- each choice needs to consume resources that, if lacking, adversely effects the player. Without exclusivity, there is only one option, or the player can simply always choose all options. 
* **Situationality** -- circumstances should weigh heavily on which choice is preferable. Without situationality, you repeatedly choose the same move once you've decided it's best.

Actions generate tension through having asymmetrical costs and payouts to others. Asymmetry of conditions leads to strong situationality.

(@Work these next two concepts in somehow)
With situationality, an action can be better or worse within a limited context, indirectly related to the game goal, based on conditions that may change. Localized value judgment + indirection is the key!

Force allocation relies on repetition as a form of indirectness. If you're required to do something repeatedly in changing conditions, that means situationality can be interposed as a source of indirectness. Multiple different instances of a problem.

## Tension in Action

Now let's bring it all together by analyzing the structure of RTSes like Company of Heroes.

The actions of building units in RTSes typically exhibit all three necessary tension-generating properties. 
* Units cost varying amounts of shared resources, creating exclusivity. 
* Which unit to build (and if you should build any right now) depends on what you've seen of your opponent, creating situationality. 
* No victory condition is satisfied by producing a certain unit--you typically have to build and move many units to achieve the victory condition--thus there are usually at least two levels of indirection. The above goal analysis of Company of Heroes shows that there are five levels of indirection in that case. 

Another core problem for the player in Company of Heroes, as with all RTSes, is force allocation. This problem arises because of exclusive positioning and localized effects of units. Guns can only fire so far, and maps are far bigger than any gun can fire. Even off-map artillery in Company of Heroes can only effect a small area of the map at once, though it can be deployed anywhere. On-map units can only effect the area around them, and can be rendered irrelevant to an important engagement through mistakes of positioning. Exclusive, situational positioning is the bread and butter of Company of Heroes combat.

The beauty of Company of Heroes, and indeed most RTSes, is in the interaction between the force allocation and unit construction problems. There are three layers of situationality at play: strategic production, strategic deployment, and tactical combat. The payout of building a unit is thus situational in a dynamic and complex way. This layering of situationality is a powerful design technique, since it tightly interlinks several interesting kinds of decisions that have partially overlapping sources of tension.

Although force allocation seems very different from force composition/unit construction problems, I hope you can see how the common conceptual vocabulary I've introduced in this article makes sense of them with respect to the designer's intentions of making a system of interesting decisions. There's a lot more to say about this topic, and many higher-level features and interactions to explore using this groundwork. Stay tuned!

[1]: http://www.gamasutra.com/view/feature/174832/the_more_you_know_making_.php?print=1
[2]: https://learn.canvas.net/courses/3/pages/level-6-dot-1-tips-on-decision-making
[3]: http://www.gdcvault.com/play/1015756/Interesting
[4]: http://www.gamasutra.com/view/news/164869/GDC_2012_Sid_Meier_on_how_to_see_games_as_sets_of_interesting_decisions.php
