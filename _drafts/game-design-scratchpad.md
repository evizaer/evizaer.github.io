---
published: false
---

# Reward specificity and strategic diversity

Assume a game with roguelike structure. The player has a character which accumulates abilities and stats throughout a process of completing multiple dungeon floors of increasing difficulty.

Typical reward granularity is that XP is rewarded with precision based on completing some small goal, like killing a specific enemy or lock-picking a chest, or casting a difficult spell. This incentives doing those things. If you find a way to beat a level without doing those things, you are hamstringing yourself. You want to engage in strategies that exploit these rewards in such a way that your character's power spikes relative to the power of enemies you expect to fact. So even though both your and the enemies' power increases floor-by-floor, you want to garner enough reward that your power increases faster.

If you were only rewarded upon going down a floor, this exploitation becomes impossible. Fighting enemies because a potential inconvenience. Enemies become obstacles instead of reward-bags. The challenge becomes reaching the next floor at minimal risk, not farming loot drops and experience from monsters on this floor so you spike your power level and can stomp through the next floor.

# Situationality

To create situationality, you must create situations. How do you build an interesting situation from the ground up? You create an environment where results are contingent on many factors, which are themselves results of prior activity which was contingent on many factors, and so on.

To start, situations require locality of cause and effect. Causes and effects can't be the same in kind or magnitude across the entire system for a actions. How do you do this? By giving player actions conditions, and by parameterizing actions using environmental factors which are also manipulable or liable to change.

An action has parameters when its costs and/or effects are based on environmental factors. In D&D-like combat systems, attacks are parameterized by weapon, location, the character's strength, the target's armor class, and other factors. Varying these parameters creates situations where actions' effectiveness strongly relies on context: hitting the dragon with your puny sword is pointless because even if it didn't dodge you would do no damage to it, so now what do you do?

On the other side of parameterization is what I call hyperintersectional gameplay. These are situations where player choices are overdetermined due to how constraining the situation is. The fighter has no option but to swing the sword, even though he knows it has a vanishingly small chance of having an effect on the dragon, because several powerful factors have intersected. There are also more subtle and perverse cases of hyperintersectional rules where a player action affords you an action that you never want to take, because getting into that situation means you're likely to lose anyway. 

Cooldowns on abilities in typical MMORPG designs are a better way of creating situationality than a mana pool. Cooldowns force the player to do something else with the time during the cooldown of their favored ability. This regularly creates a special situation where you can't actually do what you want to do, but you should do *something*. Players see the interlocking rhythms of their cooldowns and optimize ability use into patterns called skill rotations. Skill rotations are far harder to master than simply picking your most powerful skill and spamming it, and the fact that there is a series of actions the player wants to do in a certain rhythm means that the rhythm can be interrupted to create novel situations where the player has to adapt. This metalayer of adaptive play would not be possible without the situationality baked into the combat system.

In [a previous article](http://nohidden.info/tension/), I outlined three components of player actions that lead to interesting decisions: indirectness, exclusivity, and situationality. Situationality is by far the most complex of these three, and is built out of mechanisms that create indirectness and exclusivity.

Situationality arises from pervasive use of localized state change. Put related restrictions on when and how actions work, and you create situationality.

Situationality rests on a bedrock of exclusivity and indirectness. You need to design actions that have distinct effects, which implies exclusivity in the components of those actions, and these distinct effects must have sufficient removal from the game goal that their meaning is non-trivial to derive and contingent on the game state in a complex way.

Localized effects + non-transitive interactions.

## Maybe simple prototype?
We can design a simple prototype of Company of Heroes-like gameplay to see how situationality arises from small numbers of moving parts.

There are three units: tank, infantry, and anti-tank gun.

There are two terrain types: cover and open ground.

(@Does this even work!?)

## From Tension article draft

The designer can introduce additional complexity into the player's decision-making process by introducing various conditions under which certain actions change their availability or costs and payoffs. I call this "situationality"--and the easiest way to think about situationality is to think "what could've been different in this situation to cause me to choose to do something other than what I chose?" Some examples:

* 2D or 3D space is the most pervasive form of situationality to be found in games. Space provides uniform rules for having numerical relationships (like distance) between two game pieces, it allows easy-to-understand conditionals for rules, like if a unit is in range of another (for attacking), or if a unit is in range of a spot on the ground (for moving to it this turn).
* In Star Craft, only medics can heal marines, and only a medic near a specific marine can heal that marine.
* In Settlers of Catan, you can only build a settlement on a tile-intersection next to one of your roads if you have a brick, lumber, grain, and wool. You also aren't allowed to build settlements within two intersections of one another. You can only build a city if you have 2 grain and 3 ore and you already have a settlement on a certain intersection.

### Indirectness
Without some degree of indirectness, it's clear what to choose to do to win. When decisions lack indirectness, the player can easily make decisions because he can clearly see that one action gets him transparently closer to winning than the other.

Removal or indirection. Playing at several remove from the goal. Requiring repetition can achieve this (health bars in fighting games, score goals) cheaply. 
# 2v2 Teamwork in Steel Division

You can only see so much of the battlefield at once with accuracy. Zooming out helps but makes things imprecise--you have to zoom in to issue orders at an appropriate level of detail to take good advantage of terrain features.

Coordination between two people a lot harder than simply issuing all the commands yourself.

The obvious XvX strategy is to split the battlefield and spread forces into allies' territory as little as you can afford to.

Decks are balanced to fight 1v1 vs. the other decks, but Stell Dvision could've made an XvX deck system more dynamic by allowing the players to order units from any selected deck. This opens up more deckbuilding depth and more depth while playing!

# Subgoal analysis

But where do sub-goals come from? A part of learning a game is identifying important intermediate steps along the way to victory. You can come up with some such steps by reading the game's rules and noticing which actions put you close to winning. In Chess, you can quickly determine that to take the enemy's king you have to put him in check, and to do that you must move pieces so that they attack the king. So the obvious sub-goal is to attack the king. But there are other pieces in the way, so you have to invent further sub-goals to somehow get them out of the way, by either capturing or bypassing them. This process of sub-goal generation proceeds away from the end-goal and often can get all the way down to something you can achieve in a few moves--from a goal so far in the future that you couldn't hope for a forward-simulation to include it, to a sub-goal so near that you can work out its achievement in detail.

Notice that in that Chess example the end-goal was specific, and as I worked backward in time the sub-goals became less specific: from capturing the king, to attacking the king, to perhaps bypassing or capturing other pieces. Choosing how to instantiate the more abstract sub-goals is the real quandary you face when playing a game. Will it benefit me more to try to punch through a pawn wall with a concerted attack immediately, or should I aim to draw his pieces away from the point of attack first through some diversionary threats? I can come up with all kinds of sub-goals which serve other sub-goals, and many of them lead to near-term moves that are radically different from one another. Here we see the substance of what makes a better player: both choosing the better sub-goals, and being able to achieve them more reliably through accurate forward-simulation.

# Tactical and Strategic interaction in LW2

I've been watching JoINrbs streams of playing XCOM 2: Long War 2 recently. He is a balance tester for the hardest difficulty. In his streams he is testing various aggressive strategies on the hardest difficulty and failing plenty, while also learning and teaching plenty.

His strategies typically came in the form of extreme hardship on the tactical layer in the interest of piling up strategic-level rewards and snowballing into an easy late game.

Then he transitioned to trying a different strategy where he tries to manipulate the strategic layer to make the tactical layer typically a lot easier by spreading out ADVENT's attention among many regions and closely managing their level of aggro to keep enemy forces from concentrating and building up in any specific region.

His diffusal of strength approach is a sane approach to guerilla warfare which is just the kind of play the game should emphasize.

His prior testing was mostly about 0% runs on specific missions. XP is gained in proportion to number of enemies on the map. If you can succeed in a mission with lots of enemies, you get lots of experience. This can snowball you early in the game if you can get your soldiers through it.

Are the 30-day wounds you get from stretching yourself actually worth the extra experience? You could've run three normal-strength missions in that time, instead. 0%s do break the soldier time management aspect of the game, but if your soldiers are getting locked out of doing missions due to egregious wounds, you aren't really breaking the system.

 map sizes don't increase when you have more enemies on them. So not only are more enemies per pod and more pods, but it's easier to run into multiple pods at once, so your expected enemies per encounter is higher than the pod size increase would suggest.

# Guessing other players' valuation

Self-balancing and dynamic. Especially when you're choosing between set valuation schedules--if you can just guess each player's valuation and directly dial that guess into the game rules, there isn't a trade-off for doing it. Set batches of valuation guesses provide additional exclusivity and stop players from trying to be overly precise and wasting time.

Is it like guessing hidden information, as in poker?

# Betting

Put betting on any system of gradual hidden information reveal and it just works


# Indirectness in time and space

Goals can be made indirect through the use of time and mechanical space.

In time: 
* tech victory in Civ
* Controlling victory locations over time in Company of Heroes and Wargame.
* Efficiently using units over multiple engagements in RUSE

In rulespace
* Victory Location victory conditions are several actions and conditions away from direct player actions, like moving units, constructing buildings, or researching tech.
* Sensible play encourages the player exploiting positive feedback loops to increase chance of winning later in the game. This happens in deck-building games, where acquiring victory points is possible early in the game but the game rules and non-victory point cards can let you build an economy that allows purchasing way more victory points in a short period of time much later in the game.

# Stellaris vs. XCOM vs. Civ tech model

Tech models in long-campaign games.
Core features:
* Ephemerality - Techs are cannot be lost through the destruction of on-map units or buildings. (Contrast with RTSes, which have a mix of buildings as reified tech and upgrades as ephemeral tech.)
* Dependency - Techs need to be unlocked in some order--you can't just work towards any tech you want at any time.

Each individual tech research is a player action, and comes with all of the features I introduced with player actions:
* Costs - The player has to commit a certain amount of time before the tech is unlocked, and sometimes some other resources as well.
* Payouts - Techs are only valuable in that they unlock something, be it better units, buildings, or other actions.
* Conditions - Techs require other techs to be researched first. They can also be locked until you acquire certain resources or achieve certain sub-goals.

Tech trees are a source of interesting decisions:
* Indirectness - Though many games with tech trees let you win by researching some specific tech, usually it's a long way away during most of the game and the player must engage with other game systems to ensure they'll even have a chance of reaching tech victory. Tech contributes indirectly to other possible victory conditions, like military conquest and putting up special buildings, by providing conditional boosts towards production and unlocking the ability to produce the needed buildings and units to achieve those victory conditions.
* Exclusivity - You usually can only research one tech at a time, which immediately puts techs in tension--especially if they have juicy payouts. Sometimes researching one tech can lock you out of another forever, or there simply isn't enough time in one play of the game to research all techs.
* Situationality - Tech trees can be richly situational. When tied into many other subsystems in a game and with sufficient rules to enforce strong exclusivity, tech provides is a powerful source of strategic commitment. Since techs are preconditions for engaging with other potential high-situationality subsystems, like combat and building optimization, the tech system acts as a gatekeeper and facilitator of more concrete forms of situationality.

## Strategic Commitment Trouble

Tech trees that are too exclusive lead to strategic commitment. If players cannot gather enough information about their surroundings to be expected to intelligently commit to a strategy, the player can only hope to get lucky and run into enemies that their strategy counters. In this way, a poorly-designed tech tree can destroy situationality in other parts of the game by limiting the player's access to game elements enough that the player is forced to play a too-simple optimization puzzle with only a few pieces. Lacking the tools to adapt, the committed player can only hope he encounters obstacles the solution to his simple optimization puzzle gives him enough power to overcome.

Endless Space has this problem. The combat system is simple rock-paper-scissors. You only more powerful rocks, papers, and scissors with separate techs that are often dependent on earlier techs that give the same kind of payout.

XCOM: Fixed tech tree with hidden future techs.
Stellaris: Generated techs with random selection between available techs.
Alpha Centauri (Blind Research mode): Choose a focus and research a random available tech from that focus.
Civ: Fixed. All information is available from the start.
Endless Legend: Small number of tech tiers with 10+ techs in each. Can research any tech on current tier, price goes up as more are researched.

Components:
* Whole tree info
* Tech proc gen
    * Dependencies
    * Unlocks
* Tech selection abstraction
* Dependency complexity

## Design Objectives

Player can choose different tech paths for different gameplay options. Replayability may result. Dependent on if you can get all techs each game, or if you end up only getting a slice of the tech tree.

## Ideas

Tech fog of war: you can only see the next tech or two down the tree. Randomize beyond that upon reveal based on what has been researched. Allows player to see into future and form plans, but not excessively detailed ones. Assessing effects of tech choices is possible and less arcane than the Stellaris model.

# XCOM2 consumables and risk of moving forward

In the beginning of X2 missions, moving forward is most risky because there are many pods on the map you could run into and be forced to fight from unfavorable ground. So you use consumables from a safe distance against these enemies.

Later in the mission, you have few or no enemies left to activate, so you can instead use flanking shots to kill enemies because you can move forward to flanking positions without fear of running into more pods. There's also more of the map in which you know pods aren't.

# LW2 reward granularity and farming

LW2 experience is based on the number of enemies in the mission. You get additional experience based on how many enemies you killed. Usually most of your experience is for merely completing the mission.

Failing a mission can cause "shaken" status effects on your participating soldiers on the strategic level. This is to prevent going on impossible missions, farming up a dozen kills as safely as possible, then leaving. It forces you to engage more with infiltration and soldier time management puzzles.

# Move atomicity and XCOM 2's stealth

Does XCOM2 take stealth seriously?

The initial game doesn't encourage you to stealth missions. You are intended to fight your way through each map. Stealth was for creating ambushes.

What role do ambushes play? Why were they introduced?

Ambush set-up means you can move around the map with less fear of pod activation, so you don't have to do boring xcom2012 conga-lining and constantly overwatch. You have more control over the first engagement.

Timers add the time pressure needed to prevent the player from wasting too much time waiting for advantageous turns to engage by, say, blowing up a car with several enemies aroudn it to kill them all. Penalties for timer exhaustion are harsh: usually mission failure and/or loss of all soldiers on the mission.

After the player has broken concealment, usually all characters but one or two (Rangers with a certain perk) are now detected at much further ranges. (This is thematically weird--why would enemies suddenly get better vision but only for seeing certain people? A guy with a gun and a sword is no less suspicious to an advent trooper than a guy just holding a gun.)

You should be able to react immediately upon seeing enemies, because one tile matters. A unit will blunder right into enemies when it really shouldn't because it has to complete a move.

This also happened in XCOM2012 with pod activation.

The game should stop your blue move, consuming the movement points so far spent, and then let you give another blue move order with the remaining movement points, as soon as an enemy pod comes into sight.

# Poker, yomi, and interesting decisions.
Poker? THe mental game--how does it fit into my model?

When does hidden information become relevant? where is the information hidden?

In poker, info about your opponent's hand is in their mind. Your interface for querying their mind for their hand's strength is their betting pattern, which is "tested" by their reaction to everyone's bets at the table. Since you only know your own hand strength, though, during a hand the most valuable information queries involve your own bets and that person's reaction.

It's important to build a mental catalogue of bets, behavior, and revealed hand. This is made way more difficult when players who fold don't have to show their hand at the end of the hand.

Betting is compatible with any largely non-interactive hidden information system, and turns them into interesting games in proportion to how frequent and effective the feedback per bet is. Hold 'em Poker has phases of betting as small amounts of further information are revealed. Common information makes it more interesting to calculate odds, and gives the players more potentially significant information to react to with their bets.

# XCOM grenades shift costs

It's better than grenades are free, but using them to kill enemies is expensive. OXCOM makes you pay a nearly trivial cost to make them but they don't prevent gaining loot.

It's a situational concern in combat! Overall monetary expenditure must be trivial for grenades, because it has to compete with powerful abilities.

You can turn corpses into money in new XCOMs, but money is in general much tighter and on a smaller scale. Grenading an enemy has a cost that varies with the enemy!

# Leftovers from tension article

With situationality, an action can be better or worse within a limited context, indirectly related to the game goal, based on conditions that may change. Localized value judgment + indirection is the key!

Force allocation relies on repetition as a form of indirectness. If you're required to do something repeatedly in changing conditions, that means situationality can be interposed as a source of indirectness. Multiple different instances of a problem.

Some games make available activities which have make all other activities better, like improved action economy. These at first seem like short v. long trade-offs, but realizing a trade-off is contingent on being able to take advantage of your opponent's "weakness" caused by building up action economy instead of "defending themselves".


### Positioning and Space

Space is the most powerful tool designers have to create interesting decisions.

Space is exclusive: a unit can't be everywhere. Because it is in just one place, it enables situational play--staying out of its way! In a game like Company of Heroes, that has multiple victory locations and only requires a player to control a majority of them to win, one big powerful unit is not so threatening, because though it may steamroll your troops wherever it goes, it cannot be in two places at once. If you build a strategy around striking where it is not, you will win. Due to the exclusivity of resources, that big powerful unit represents a lot of the resources that the opponent had access to. If you deploy your troops against whatever else the opponent has, you should have local advantages.

Local advantages are the stuff of good gameplay.

### Exclusivity
The player is forced to make decisions when she can't do two things at once. It could be because of any kind or combination of resource constraints: time, minerals in Star Craft, fuel in Company of Heroes, or even the player's attention. The option she chooses brings her closer to some sub-goals while making others harder to achieve. Regardless of which goal she's pursuing, a decision should shift her orientation and progress towards (and away from) many potential sub-goals at once. I will go into more detail on how this works shortly.

Exclusivity is differentiation--exclusivity is at the heart of all trade-offs, and usually it'll be exclusivity along many dimensions. Not only can you only do one action on your turn, but the actions don't even effect the same areas of space and increase or decrease different resources in various ways.

It's more than just having multiple actions of which you can only take one. The actions themselves should have exclusive effects and costs. Actions that can be directly compared based on their effects are of no use in creating tension. Two actions  that give different amounts of the same resource for the same cost are never worth having. If two actions end up being effectively the same cost for different magnitudes of result, it's well worth it to find out why and see if you can prevent that from happening. Don't waste the player's time.


### All Three, Working Together
Dimensions of exclusivity can stack to create real tension! Choosing whether to heal one unit for 2 HP or another unit for 3 HP has directly comparable cost and payout at the resource level, but they have exclusivity baked into their conditionalty--the unit to which each applies is exclusive. Games where effects are localized feature this kind of thoroughgoing situationality which lays the groundwork for lots of tension.

Indirection is what makes unit production in RTSes interesting. It's hard to value a specific unit because its ability to do its job is highly conditional. Can you protect it long enough for it do damage? Can you get it to the right place to deal damage before counterplay is possible? 

Exclusivity in time gets you nowhere alone, it is a structural support for trade-offs, though. Without it you cannot have trade-offs.


## Simplest example?

Linear race game vs. circular race game. In linear game, value to move to a space is clearly its distance to the goal. Players can't meaningfully interfere with one another, and there's no reason to use exclusivity in time or space because interference is a direct trade-off with achieving the goal sooner, and you can't sufficiently interfere with your opponent for the interference to be worth it--probably ever, even in 1-piece-a-side. 


## The Constructive Approach

The idea of tension is intended to be useful when you're designing a game. I intend it to be a pattern against which you mentally test rules as you think of adding them to your game.

When designing, think of what the hodological space of your game looks like--that is, think about what a player will want to do based on the goals and tools you're providing them, and how they can use the game rules to reach those destinations. You can think of hodological space as a heat map overlaid on the game's rules which lights up in groups of rules that the player that the player is strongly incentivized to use, and is cooler in areas that get rare attention from the player. If players are using some of their actions way too much in proportion to others, or leave entire subsystems of the game unexplored, you need to adjust the rules to adjust the player's incentives and push them towards using a more appealing balance of the tools available.

In order to adjust incentives intelligently, you need to have a mental model of what a player wants and doesn't want in your game. That the player wants or doesn't want to do something is the result of many complexly interactive factors which may themselves be complex. 

The most obvious case--and that which generates all others--is that the player will win if he chooses a certain option. Such an option will be chosen immediately if recognized. If there are multiple options which will cause the player to win right now, it's irrelevant which the player chooses. (@Further explanation of why RPS isn't like this) These cases do not present the kinds of trade-offs which comprise interesting decisions, and situations which closely resemble this will also not register as interesting.



Strategy is using limited resources to maximum efficiency during a limited period of time in achieving a goal. What's the general structure of the efficient use of resources in a period of time? 

(@Probably a bad paragraph)
The player's approach to forming a strategy has to do with addressing the influence of various conditions on his ability to win the game. When first acquainting himself with a new game system, the player is confronted by a jumble of conditions which change his ability to achieve his goals. The process of learning the game is untangling this jumble and slowly reducing the number of conditions the player needs to take into account in his evaluations. Better strategies in part consist of heuristics that reduce the cognitive load on the player by highlighting those conditions, out of an overwhelming manifold of conditions, that are worthy of close attention.

It's this reduction process that allows a Chess player to decide to sacrifice a pawn in order to improve his center control. The concept of center control is itself a way of reducing the number of moves to forward-simulate through elevating the value of moves that exert control over the center. The idea of control is also a reduction mechanism at a much lower level, since it gives the player a tool to think in the abstract about possible future states of the game in terms of the movement patterns of pieces.

## Short-term vs. Long-term

One of the most pervasive tensions in strategy games is short-term vs. long-term. 







## What are we abstracting over?
Is anything used by players in the game to achieve the goal a resource?

A resource - any game element with outward edges on the production network.

@Revise: production network, not resource conversion network? Then I can define resource in that context. Production is just a direct result of rules in operation.

The structure of strategy games: goal-directed resource conversion. Games have a multi-level structure of resources which at its root are simple, abstracted, resources that do not directly make progress towards the goal (minerals in SC). At the highest levels you have resources which directly accomplish the goal.

Engine games typically use the same resource to either multiply itself or create VPs. You multiply resources as long as possible, then transition to VP production. This requires a positive feedback loop on the resource used to acquire VPs, and that there is a basic resource that is used at both the beginning and end of the conversion network.

(@Todo: Make conversion network diagram for Dominion)

SC conversion network is targeted at destroying your opponent's conversion network. "Annihilation" victory conditions in strategy games are about the total destruction of the opponent's resources. Total destruction overdetermines failure, or loss, by requiring way more to be done to defeat your opponent than is sensible for them to come back from.

But what about space? Resources typically have some kind of accumulation into a one-dimensional space where more is "better" in that it lets you linearly convert into more of some other resource(s). Space is different. Space is all about differences between pairs or triples of numbers determining access to abilities and effects. Space is a resource, but only in how it relates to other items positioned in space. Players spend time and other resources to expand their influence over space on a game board.

You typically don't "pay" for things in space, but you do pay to be within a range of space that enables new productions.

Space is the most powerful tool for situationality.

## Conversion networks
Sequencing to maximize effect.  Player actions put resources into conversion networks which mature at different points in the game. 

Maturity means yielding a "pointy end" with which to pierce the win condition. Usually this means there are preparation phases and exploitation phases. You build an army, then you use it to damage your opponent's capacity to damage your capacity to damage them. (What about Company of Heroes and point capture?)

Strategy games are about giving players interesting choices.

Each interesting choice exists because the game presents exclusive actions that may work towards objectives that are both valuable but either exclusive or compete for the same resources.

Opportunity costs. Especially when those costs persist. If you have access to the same choice multiple times then the opportunity cost doesn't matter much, since you can just take it next turn.

To understand how to generate interesting choices, you need to understand how to construct a system with its pieces in tension. You want to maximize this tension and make it as complex and multi-layered as possible--such games maintain their interest for longer.

Complex tension means variations in contextual elements change what you have to do, sometimes significantly. You don't always want to do Action A, you have to do action A when X and Y are true, and action B when Z is true and C just happened, etc. The more twists and turns this stack of conditionals is the more tension and interest.


## Situationality

The player asks "What could I have done differently?" when he loses, the designer asks "What could have made the player do something differently?" and "What could make the player use X instead of Y?"

What's interesting about a situation is how it's different from all others--that's why you'd want to look into what happened in the first place! There has to be similarity between situations, which allows orientation, and then there have to powerfully-contrasting unique bits.

## From nothing to something: Interesting decisions from scratch

The simplest (and utterly degenerate) game is a single-player game where the player can either directly choose to win or lose. This game only provides one possible measure of utility of a move: if it wins or loses. We can evolve this base case in one of two directions to try to generate some interesting decisions for the player: we can introduce randomness to obscure the outcome, or we can add some parallel systemic continuum separate from win-loss that the player has to make decisions about which indirectly leads to the determination of if they win or lose.

The randomness approach suggests the simple elaboration of asking the player to guess the outcome of a coin toss. This game gains uncertainty in the result but sacrifices the player's ability to exercise skill. There is nothing relevant to the result to discriminate. Sure, you can make a choice between heads and tails, but it only has an incidental (@what does this mean?) impact on whether you win or lose.

The determinist approach doesn't directly suggest anything obvious to me--you could go in several directions. One direction is a packing problem, where the player is given a list of numerical values and has to find the combination which sum to a target number.

Obvious determinist approach is just to add more branches. Choose 1 or 2, then 1.1 or 1.2, etc. Then these map to winning or losing directly. This adds one layer of indirection which is trivially surmounted by thinking ahead by one action. The win or loss determination propagates up the decision tree, from the end of the game to the beginning, directly and clearly.

(@More: This is introducing a layer of situationality into the decision tree, but we actually want to introduce it into the valuation algorithm! Multiplying states doesn't necessarily have an impact on valuation. situationality with stark results is important)

Now introduce a resource: Z. You can choose whether to have one more or one less Z each turn. You win when you reach a target amount of Z. Still not interesting, though, because you have no feedback. If you know the rules of the game, the path to winning is obvious, if you don't know the rules of the game, the path to winning is totally obscured--just don't retrace your steps by adding when you once subtracted Z, or vice versa. Contrast this to a game where you MUST arrive at a target amount of Z using so many additions without a subtractions.

## Misc notes

Indirection is implied by clashing incentives. Games have one incentive: to win. To have clashing incentives, there need to be many contributing effects to if you win or not. Chess accomplishes this by checkmating requiring the interactions of more than two pieces--thus you need to balance the incentive to put multiple pieces into necessary checkmating positions--you want to put a bishop here and the queen there, but you can only do one at once, and your opponent will have time to react and potentially make it impossible for you to do the other move you need to do!

### Layers of Indirection: Company of Heroes Example
To produce multiple conflicting incentives, the designer can simply add more conditions to winning. Scoring along more than one dimension introduces a trade-off between advancing along the dimensions so long as the dimensions are built out of different stuff.

Games with higher sophistication add layers of indirection between the stuff of the victory condition and the stuff the player can manipulate. In Company of Heroes, you have to accumulate a 500 victory points to win, which is done by holding more victory locations than your opponent over time, which is done by moving infantry within the capture radius of one of three points, which can be done once you build troops, which can be done once you build certain buildings, which can be done using your starting engineer units and starting resources. So many layers of indirection!

There are four main layers here: 
(1) the layer of victory points. Introducing an element of time during which control of territory is contested. 
(2) the layer of territory control. Introducing methods of removing an opponent's units from areas of interest.
(3) the layer of unit manipulation. Introducing the ability to put units in places on the map which are better than others towards achieving victory. 
(4) the layer of unit production. Introducing buildings and units, which are ways to spend the resources of manpower, fuel, and munitions towards winning.

### Relative utility of resources, regulated by feedback loops
Linear growth is the enemy of good game design. The enemies of linear growth are positive and negative feedback loops. Negative feedback loops force the player to trade something for linear growth. Positive feedback loops provide relative spikes in utility that cannot be sustained without every-increasing resource consumption.

Games must be linear in resource gain to avoid exponential utility growth via positive feedback loops.

XCOM: in-mission resources are primarily lost. Resource gain is only relative. Looking for gains in EV of ability use compared to enemies. Gun ammo is cyclical, and not lost. From a given position you can calculate EV of each ability's use on each available target. EV components are ammo left (minor), enemy HP left (major, especially if it kills an enemy). Reward for killing an enemy is lower expected damage received, which lowers rate of player losing units. Having more EV than an opponent thus leads to a positive feedback loops of eliminating opponents which lowers overall enemy EV while reducing expected loss. Lower expected loss means more risk can be tolerated and thus more damage can be done faster. (ex. when you know you have enough actions to kill all remaining aliens with 100% certainty, you can run guys into cover--it collapses negative consequences by removing threats.)

### Misc.
The ways you elaborate a game are to add additional conditions to requirements and add additional conditions to payouts (benefits AND costs!) for meeting the requirements. That's basically all.

Want to introduce situationality without overdetermining player action through copious restrictions on what can be done, or what can be done with obvious benefit. Proofreading can result from excessive sharp situationality.

Always-good options have no tension.

Tension is a dynamic property of a system which generates interesting choices for the player.

Tension is a way of articulating when a design is sufficient to support non-trivial strategy.

Short-term vs. long-term relies on the same as risk v. reward, except long-term is obscured by all of the unknown decisions between now and then, whereas risk v. reward can be compressed into one dice roll.

Where uncertainty and ambiguity match up and diverge. It is not ambiguous whether you should choose a move that gives a 75% chance of winning or a move that gives 70% chance of winning. But it is uncertain whether you will win.

Two most basic tensions:
Opportunity costs
Short vs. Long term

SwiftSpear suggested Mass vs. Rush vs. Econ in SC.
Probably is potential vs. reality, or flexibility vs. manifest power. 

non-transitive interactions heighten the tension caused by opportunity cost.

Understanding the properties of rulesets, then designing to achieve certain properties while avoiding others.

# The role of fixed points and discreteness

The units in a game like Star Craft or Company of Heroes represent discrete points on various stat-per-resource graphs, like attack-per-mineral or AP-power-per-fuel. We often talk about these power curves as a tool for addressing game balance concerns, but it's worth examining why we make these fixed points instead of providing a power curve and letting players pick a point on that curve for the units they want to build.

UI is difficult, perhaps impossibly-so.

Discrete points ensure there's imperfection in mappings--the player always overshoots or undershoots. (Maybe not actually valuable?)

Less cognitive load to manage the combination of some pre-set resources. Perhaps too much indirection?

This is a general case against unit customization. It could be read as support for sufficiently discrete customization, though.

# Comparative analysis of XCOM vs. Battle Brothers combat

Reference videos from Marbozir and XWynns or Joinrbs

XCOM abilities have tons of contrast.
BB abilities seem to move stats around.
Cover and flanking provides large positional contrasts with sharp boundaries. BB terrain just gives a bunch of penalties or bonuses that are non-situational.

BB doesn't seem to have any concept of shock, so attacking is just a disadvantage since it weakens your formation and opens chars up to ranged attacks.

A further contrast with FFT 1.3 combat might be awesome.

XCOM missions involve engaging multiple pods. With a timer, finishing off enemies efficiently is at issue--without a timer it doesn't matter since time is unlimited. (You can delay and use renewable resources--bullets--to do the work.) BB is single-pod, so battles peak in interestingness pretty early and whimper to a conclusion as one side gets whittled down.

# Civ 6 and AI in the face of exponential advantage from non-trivial system optimization

Civ 6 city layout is now very important, and can have huge benefits for well thought-out city, district, and improvement placement. AI is hard to write for this, so the player can easily gain a huge advantage as the game progresses. Even on Deity, as Quill18's latest LP shows, the AI gets a huge head start but superior layout ensures the player can catch up by halfway through the game. Snowballing mechanics are worsened by an AI that can't go from linear growth to exponential and thus goes from being overwhelmingly powerful for a third of the game to being a walkover for the latter half.

# CoH vs. SC

CoH's VP system allows it to disengage the positive feedback loop of the zero sum nature of annihilation. This allows both players to remain capable and capable of recovering from blows throughout the game. CoH has further made base rushes much less profitable by providing free base defenses that are potent against early-game units. The retreat system also leads to plenty of units being at your base if you're in a position where a base rush is available to your opponent, so the many weakened units can usually take out the threatening unit.

# Complexity and slack

High complexity requires more slack. The game won't permit learning if there isn't enough slack so that the player can explore the complexity without being pummelled. This is a good reason to have multiple scenarios, or to keep complexity from getting too high.

# XCom research, time tensions

Should it be hard to equip all soldiers with latest equipment?
Moving swiftly through research means you can't pin down strategies for the tactical layer. A cheap way to avoid the player running out of tactical depth--just give them different combinations of techs to work with against evolving enemy types.

# XCom strategic layer hidden information
Tons of hidden info early on. You can only see in such a limited range that the alien activity doesn't have much meaning and it's hard to make good decisions. This is also when you are worst-equipped.

Later in game you have good radar coverage and can make smarter decisions about when to engage, but you also have more capable and customized soldiers. 

This is another bad feedback loop in the game.

It's also a "newb trap", because the newb's ability to comprehend alien behavior is worse the newer he is because you start off with the least amount of information and then have more as you get through a campaign. Many players can never interact with the real strategic layer depth because of this lack of informtion. Since other positive feedback loops can cause you to start steamrolling aliens before you can even piece together alien behavior, the strategic layer's intricate logic of alien behavior is largely unnecessary to explore, and thus should be removed or tweaked.

# XCom 2 design work
More conditions and ways of manipulating the timer.
Timer needs to have conditional bad meanings for when it expires.
XCOM's goal is to fight as few aliens as possible--this is a guerilla war after all.
XCOM's tools should make engagements conditionally go by faster, if time is the key here.

You NEED interleaved turns, or else opponents just do not get a chance to act, so interaction with them is much more flat--you can only modify conditions for killing them, you can't also have them effect how the mission plays out further (??). It just increases resource costs (these resource amounts don't matter until they're 0, and most have more than 1 use) to not pay a time cost.

Bullets are free. Abilities are not. This is important to the cost structure--bullets have to take more time than abilities, but also bullets are more likely to miss. ABilities just give you certainty, and certainty is really powerful because you can KNOW how much time it will take you to move past a pod instead of merely having some probabalistic estiamte.

Slowness of XCOM1 would go away if enemies converged on your position by default, so if you don't move enough you will get slammed by pods. This may overreward defensible starting locations. Perhaps pods patrol "aimlessly" until the first engagement, then they go on a yellow alert. Long War 2 has this yellow alert and it seems to work well, though free actions for enemies don't feel good, since enemies usually just pop out of fog of war and start shooting you--bad near randomness.

Why not let the player see all terrain and also give them motion tracker at all times?

Watching Long War 1: number of times player relies on AI being bad is crazy.

# Force allocation in TSes and RTSes
From DO discord convo with JP:
RTSes and Team shooters (TSes?) both present similar problems of force allocation to players, but TSes require collective dynamic solution usually without communication whereas the player tends to do all the allocating in RTSes on their own. In RTS team games you get closer to the collective action of TSes, but not very
Since it's easier to project force throughout an area of a map in an RTS, you can more easily split the responsibility for map control along the midline of the map between you and your teammate.
In a TS you can only project force in a small area.
and it all emanates from one point. RTSes allow you to project force from many points which are disconnected and potentially spread out over a broad area
So there's both a multiplication of player count, as well as a diminution of projection of force. That combines to make TSes with multi-point game modes extremely engaging and replayable.
Note that those two factors also force teamplay in TSes by preventing the clean separation of responsibilities team play in RTSes allow

# Games for testing models

Incetives align nicely for designer and modeller. Simpler model means easier-to-implement game.

# CK2's Problem

Level of representation doesn't match with level of abstraction. You "play" as a noble, but you are actually at a level of abstraction above the individual. You make decisions as if you were one noble, but your incentives are at the lineage level. This is a fundamental design failure that leads to CK2 being too easy or only hard because of punishing randomness.



# Turn systems
Alternating vs. interleaved

Complexity level: number of units to move.
Incremental feedback
Reorderability of moves, undoing stuff.

Skill and being able to react: much better in interleaved turns.
Tighter interaction is more interesting?

Reaction fire in XCOM/semi-interleaved turns. Reactions in general: a bad idea? Too complex? What's their value?

# Abstractness of rewards
A good example of this is archetypal roguelikes and XP.
Binary goal for a roguelike level: get to the stairs down and leave.
But because XP is only awarded through fighting in almost all these games, and leveling up is necessary to stand up to tougher monsters, you pretty much are forced to fight monsters even if it's unnecessary for reaching the goal

Roguelikes would see a lot of benefit from awarding a level when you hit the stairs down, or somehow  only having character advancement trigger on that goal completion. That way you can use whatever tactics you want to get there. The coarseness of the reward significantly increases count of viable strategies.

Points are interesting, because they are extremely abstract.
You can pile anything into points.
Points can even have non-transitive interactions. Like RPS points, where at the end of the game if you have more R point than they have S points, you beat them, but if they have more S points than you have P points, they beat you
You want points to be damn abstract, I think.
That allows you to have different paths to getting them
or it's a result of you having many paths
a "concrete" points system is just doing one thing generates points. Like bumping foxies onto one tile in Auro
an abstract point system rewards a pattern of play, or multiple patterns that do something similar.
Like in Company of Heroes you gain VPs by holding two or three out of the  three victory locations
that's an abstract way of rewarding players for holding territory, which itself is an abstraction over having units that can kill enemies in a specific area
which is an abstraction over movement and production of units

# Space
All variables that are a part of game state can be conceptualized as space.

Space is a predefined regular relationship between one or more variables. Strategy games typically make space discrete by making the smallest unit of traversablable space be scaled to the items in the world--say, a tile on the game's map is the size of one character or formation of soldiers (often, even larger than that).

* Space is very cognitively efficient.
* We can concoct spatial representations of more things than we currently do, like the mental state of a character. (Use RoTK10 debate system as an example.)
* more complex adjacency relationships can be represented by space very readily. Typical adjacency relationships are one-dimensional and are better represented by numbers.

# Concrete and Abstract Design
The ability to effectively generalize is a sign of higher intelligence. It's always harder to create an abstraction that captures only good things than it is to create one, concrete, specific good thing.

when the game is designed more concretely and the designer is good, the game is better at the cost of replayability
Designing more abstractly is harder.
So a good designer will usually do a worse job at it.
So you'll have higher highs when you design concretely, but the duration of those highs will be shorter because it can't really have replayability and maintain the concreteness level that allows it to be so good in the first place

# Of state and actions
To talk about the structure of games at the finest level, we need to talk about state and actions.

## State
Games consist of taxonomized objects that contain state. The game's state is all of the states of the objects in the game taken together. An object is one or more piece of state grouped together in a convenient way. You can think of state as describing what objects mean at a given time to the game.

### Dimensions
We can describe the state of a game object simply by listing its properties and their values.

A piece in chess may have the following state: `{ type: bishop, x: 3, y: 1 }`. This expression completely defines what a specific piece means at a moment in a game of chess. 

Contrast this with the state of a soldier in XCOM:
```
{
    type: soldier,
    class: heavy,
    spec: gunner,
    will: 90,
    aim: 75,
    name: Jeremy Johnson,
    x: 10,
    y: 15,
    HP: 5,
    skills: ...,
    equipment: ...,
    poisoned: 3
}
```

That's pretty complicated, even considering I left out a big blob of state contained in the skills and equipment of the soldier.

Notice that I show that the soldier is poisoned by just putting a number in its state. This is just the number of turns left on the poison effect, but that effect itself may have state, like the kinds of penalties it applies.

Win and loss conditions are simply queries of the state of the game that can be successful (leading to a win or loss), or fail (meaning the game continues).


# Far randomness? Not so fast!

* Map generation in DCSS. Multiple stairways down is good because going down is near randomness (quick exposure to nearby enemies that could be very dangerous). Blind corners make map gen randomness more near than far. Discontinuities in information reveal.


There is one key concept you need to master in order to gain a significantly better understanding of how to effectively use randomness to achieve variety in game design at minimal cost to agency. You need to analyze the effects of randomness through identifying discontinuous results.

* (@ Maybe don't do this here) Nature. How big is the effect of randomness? Does randomness choose between values along one dimension, or does it have a composite effect? Does randomness choose what a player can do, or does the player choose how to employ randomness?


# Calculation, Valuation, and Mental Models

The player's job is to figure out what they can do and what it will mean in terms of achieving the game goal. This is done through mental simulation of playing the game, and valuing the results of some amount of simulated play in terms of the goal. After seeing this game or similar games played many times, players build up heuristics and general mental models that they can use to skip a lot of mental simulation and rapidly widdle down the list of possible moves they can make to a much smaller list of moves that they then simulate and assess directly. This mental simulation is typically called "calculation" or "reading." I will use the term calculation, because I'm used to using "reading" to mean assessing an opponent's mental state in games with double-blind decision-making. The proces through which the player assesses the relative value of calculation results is called "valuation". 

It's useful to think of how the rules of a game will effect the player's mental model of how the game works. When a rule suggests the player will be getting closer to winning, the player will default to jumping on that as fast as possible. Rules that indirectly effect the goal or the means of reaching the goal are more difficult to grasp, generally, though after playing several games players will build general models of how to build up an "economy" so that they can become powerful just in time to win, and other higher-level strategic concepts useful to quickly comprehending indirection. Mark Rosewater's concept of [Lenticular Design](http://magic.wizards.com/en/articles/archive/making-magic/lenticular-design-2014-12-15) suggests that the best game elements have both a surface-level use that's obvious to beginners, but then a deeper, more powerful, and less direct use that reveals itself to more experienced players.

The player's mental model contains both the apparatus of calculation and valuation. The player can only calculate effectively when his model of the rules is accurate enough to 


# from a DFF post.


But I think there's a further distinction to make here: quantitative results can have continuous or discontinuous effects. By this I mean the difference between killing something and just lowering its HP in a game where HP has no other effect. The valuation function for the outcomes of this randomness have an enormous discontinuity at the point which damage = remaining HP. This big, immediate jump in value seems far worse than a random damage result that changes the mean time till killing an enemy from 3 turns to 4. The distance between the randomness changing the game state and the discontinuous change in game state value is the crucial element. You want the randomness to feed into several turns of decision-making, in which its effects can be mitigated, instead of making the big jump in board value suddenly and wholly because of a randomly generated number. The big jump definitely requires a reaction from the player, but only after the fact since it's over so quickly (perhaps without any reaction possible before the big jump); the agency the player has in the result is way lower.

### Taxonomy

Above I merely gave each object a piece of state called "type" which told you what it was, but thoug rules refer to that type directly, they often laos apply to groups of objects in a hierarchical way. 

In Chess, pieces cannot occupy the same tile. Pawns, Bishops, Knights, etc. are Pieces, so the rule applies to them all. Games thus have a kind of taxonomy of kinds of objects built into them. This is handy for expressing rules that apply to different game objects along various cross-sections.

## actions

The game also has rules which describe the changes the system goes through when prompted by the player. The player has a restricted set of actions she can use to transform game's state. 

Actions are themselves restricted by state. You can't order a panicked soldier in XCOM to do anything. 



# economy of mental energy
Town mgmt games are a design trap because it takes a lot of difficult design to get them to function passably, and often players derive more enjoyment from when they malfunction (crazy character behavior) than when they succeed at presenting ubiquitous AI.

It's important to think about your own mental capacity when designing games. What will be hard to understand and balance? How much complexity can you handle?

Build a very tight game with small numbers means it'll be very difficult to tweak things without throwing the whole game further out of balance.

# Characteristics of randomness
    Directness or closeness of effect: Direct effect or close effect randomness means it's very close to the player's action and happens in the determination of an action's effect--perhaps their action's results are directly decided by dice, like a damage roll or a to-hit roll. Less direct randomness is caused by the player's action, but as a secondary effect, for instance when you refill the common cards in Ascension. Direct randomness in Ascension would be a card that gives you 1d2 runes to spend. The most indirect-effect randomness possible is some set-up randomness that happens before players make any decisions, and that can't favor the first player to play. Perhaps this is the equivalent of the input/output idea?

    Regularity of randomness is how reliable it is that randomness will be used to resolve something. If multiple mechanisms that the player uses to achieve the same goal exhibit different levels of randomness and perhaps some are deterministic, randomness is irregular. If the player can choose to do some things that are random or other things that are deterministic, randomness is irregular. If all randomness proceeds at predictable times that are a matter of regular procedure and are not the result of player actions, that random element is regular. Refilling the common card pool in Ascension is regular randomness, your choice of what to do with a character in XCOM on its turn is irregular randomness (movement is deterministic, some attacks are deterministic, some are random).

    Gamut is simply how big the effect of randomness is. You can think of this in terms of how many important discontinuities randomness can cross. Being able to remove actors with randomness is a big discontinuity that randomness straddles in most games. If you're just randomizing which piece you get next in tetris, that's relatively narrow-gamut (perhaps this is debatable). Narrow-gamut randomness is not terribly common--I think we'd typically just compare two random elements and say which has a wider gamut.

    Valuation-neutrality is how much random effects alter the value of a player's current position (in retrospect). More often I think the opposite is what we would discuss: just how Valuation-biasing randomness can be. I.e. does randomnses show a bias towards a certain strategy. So if in XCOM an alien shoots at you and randomly destroys your cover, that's very valuation-biasing. Even the map generation in Settlers of Catan is mildly valuation-biasing because it may screw players who go later. The only valuation-neutral randomness would happen before all player decisions are made, and the game would have to be simul-turns to prevent all first turn advantages derived from those random elements.
     

# Instead of arcs
I don't think [arcs] describes how to make actions throughout the game matter.
Here's how to make it happen: have the dynamics I listed above happen to the dimensions that players manipulate when they act. (feedback loops, resource exhaustion, compounding advantage, etc.)
So you have powerful actions having an impact over a period of time, but because of negative feedback loops, the game tends to return to a state of equilibrium (or something like that) and players need to convert that temporary advantage into some other dimension to actually win.
By dimension I mean resources in the most expanded sense. So that includes action cards, workers to place, whatever, as well as it does what we conventionally call resources
So you have natural undulations of player power level which cause something like arcs to form emergently
Players can't avoid these undulations because they are the costs of powerful actions.

State reset is one element of the concrete cluster of thoughts that stand in place of arcs in my mental model of how games work
Also: positive v. negative feedback loops and compounding advantage
all of these things tie together state changes in the more than immediate future.(edited)
resource accumulation/exhaustion is another one.
Hm. So the word I used to use to describe how the game is broken into seemingly discrete segments is "phasing"
But "phase" is just a label for a discrete segment of time that's divided from others by the nature of the streatgizing involved. It doesn't necessarily indicate some full cyclical thing
Phases have a fractal structure, but there's no such thing as a game-long phase. Phases exist in a kind of hierarchical relationship with one another.
Like in Agricola you have a worker placement phase which consists of individual players alternating specific placement phases. This fits into the phase of a single season, which fits into the generally phasing of when you have to feed your family.
Multiple phases at a lower level comprise single phases at the next higher level, which themselves combine to comprise higher level phases.
That's structural phasing you can assess based on rule analysis.
Then there's the phasing of play. Like early-, mid-, and late- game in chess.
Those aren't rule constructs, but recognizable segments of play that are identified because they each have a distinctive character, even though they eventually blend into one another as the phases change.
I don't use "phase" as a term a lot. I don't think it's the best word for the concept
It's just segmentation.

# leftover from analogy design methodology article

This is quite a powerful method of brainstorming. The designer can chain practical mechanical decisions into analogical justification into its implications to suggest further mechanical additions and begin the loop anew. They can start this process from just about any bit of their game design and suggest wide-ranging changes that are only limited by the imagination and originality of the designer. This is a useful design technique, but it requires you start somewhere.

Most designers start with a prototypical copying approach. Take structural properties of other games that you liked and copy them, filling in the various extension points they naturally offer with different details. By using an anological chaining technique as I demonstrated above, you can break free of the broad strokes your starting point gives you and move into uncharted ground.

One entry point into uncharted ground is addressing mechanical weaknesses of existing games. I'll be working on many different  tools for understanding how to form mechanically solid game systems. Using these techniques in combination with analogical chaining will lead to some pretty strange and unique results that none-the-less have solid-feeling game worlds that are as unique and deeply interconnected as the systems that give them substance. I'm hoping to arrive at an approach to game design that offers a whole-game approach where analogy feeds on mechanical strength which feeds on analogy.

## The Crucible

The true crucible of game design is the player actually playing the game. We now lack the tools to do much else but heavily rely on this crucible. Designing a game without extensive playtesting seems absurd these days. It shouldn't be, and by advancing the art we can change this. The typical process of the game designer is to recognize in a playtest that a player is engaged in behavior the designer doesn't want to encourage--perhaps simply being bored, or perhaps becoming aggressively hostile to all other players in what should be a cooperative game--then to try to make changes to the game rules to encourage a desired kind of behavior, or to make the negative behavior impossible or too costly for a rational player to pursue. The designer doesn't know if she's found success until the next playtest shows some change in player reaction. But player reaction itself is inconstant and sensitive to many influences outside the game. You don't want to start redesigning half your game because Dave's cat died earlier today and some mild prodding from Anne during his turn caused him to break down in tears. A bored player could be simply distracted by some personal issue. A player who seems enthralled and is working very hard to win may just be trying to impress a love interest and actually they're just happy to be near to someone they have a bit of a crush on. With our current limited understanding of game design in the abstract, designers can easily get trapped into poor design decisions because of the inexactitude of their own understanding of what success looks like, and the vicissitudes of their player's lives during one of a limited number of playtests.
# The stuff of design

"Stuff that is important to know about and you should be actively considering this stuff when you make any design decision" is maybe even better than guidelines, and I think you can do it well without making direct reference to existing games.
Because we don't have that stuff.
I think it's all intuited by individual designers based on their experience playing games and cataloguing what similar games feel like to play.(edited)
What I'm describing is really about nailing down the methodology of design, instead of focusing necessarily on what the results should look or feel like.(edited)
"Think about X and be able to consciously control it in each design decision"--then once you have that down you can start following guidelines because you actually have enough control to consciously follow the guidelines.

It's about positive/negative feedback loops, reward structure and player motivation, inherent complexity and cognitive load
calculation and heuristics
and all of the bits and pieces that feed into those higher level ways of conceptualizing how a game works

# The AAV Paradigm - Introduction

Strategy game design develops and balances three important aspects which are often at odds, but also can bolster one another when combined in certain ways.

## Agency

Without the player's actions having some meaning within the game, it's not worth playing the game.

## Analogy

Without the outside world to provide substantial meaning to the abstractions of a game, the game seems trivial.

## Variety

Without enough to try and do within a game, we'll quickly grow bored and move on.

# Hodological space
hodological space n. In the topological psychology of the Polish/German-born US psychologist Kurt Lewin (1890–1947), a special form of topological geometry in which paths and vectors are defined psychologically, the distance between one hodological region and another being not the shortest path but the path of least effort given the attractive and repulsive valences of the regions making up the space. See also principle of least effort.

# Agency (unused bits)

* Agency is in the player's mind
    * People default to thinking they have agency in whatever they participate in. Evolutionary biology of the mind, etc.
    * Seeing your actions have an impact is holistic. Interface juiciness matters.
    * When learning a game you have diminished agency because you don't have the groundwork for understanding what's happening.
    * Agency is all about the player forming causal chains from their actions to goals they want to achieve.
* Meaningful participation
    * You can locate yourself in causal chains.
* We can approximate agency
    * Compare player's input to effects in the game world tha the player can see.
    * COmpare directly observable effects of player input against what the rest of the system is doing.
    * It comes down to tracing causal chains.

A player's sense of Agency is easily fooled. Figuring out how much agency you have is a learned skill which people generally find mixed emotional results from honing.

People come to an understanding of their level of agency in a situation with exposure to games. Games with no agency involved, like betting on dice rolls, or Shoots and Ladders, entertain children and some adults if there's money on the line.

Since agency is in the player's mind, even simple and unsophisticated games like Tic-Tac-Toe permit agency for children and adults who are unfamiliar. Agency is about generating the feeling of meaningful participation in shaping a game's outcomes, thus the individual player's knowledge of the game always plays an important part. Game designers needs to take this into account and try to rapidly get the player accustomed to the game enough that they can see the at least some of the causal patterns that inform decision-making and let the player make sense of the results of their input.

Player action needs to matter within the system and be a central aspect.

Let's tease apart the elements of agency:

1. You can try to achieve your interests through manipulating some points of contact in the game system.
	1. You may have an avatar in the game world to represent you.
    1. The game system may permit unintermediated interaction, as in Starcraft.
1. The game relays some feedback to you regarding the impact of your actions that you can interpret as relevant to what you've done and your interests.
	1. The feedback needs to be significant enough that you can establish causal relationships.

So first we have to look at if an individual piece of input is validated by the output the game presents. This means tracing the player's expectations and checking them against the possible results in the game next time his input is needed. Not only does the game need to show mechanical effects of the player's input, showing "juicy" graphical cues can also be important. Not many players are going to tease apart the analogical from the mechanical here--providing an interface that feels good to use can amplify systemic agency, or fill in, to a limited extent, for where systemic agency is lacking.

Strategy games where the player commands simulated people doing things, like shooting aliens, use randomness to simulate the impact of the skill of the simulated people. Often this leads to scenarios where the player gives a command, but in the game world the associated action is only performed partially or not performed at all. For instance, in XCOM you tell a unit to attack, but the attack misses. The only way that you know the game isn't ignoring your input is that an animation plays and the unit's ammo is decremented for the weapon it fired. Here we have the interface reassuring the player that their input mattered, even though the result of that input was a non-event.

When we talk about agency in game design, we use it to describe the subjective experience of the player being able to project her will onto the game’s systems. This implies that games must present a system, and that games must allow the manipulation of the system in some way by some kind of player. If a game has a system but fails to present it in a way that a player can recognize, agency becomes impossible. Agency is a trait of the player's experience, not the game itself. Agency requires a chance for player input in the context of the system and feedback that reflects that input. The feedback doesn't have to be unambiguous and the input doesn't have to be unambiguous. Without a chance for input, you don't have any capacity for the player to act (or play) so agency becomes impossible; without feedback that reflects input there's no indication that the player has taken an action, so the causation-finding circuitry in the brain can't find purchase and the player doesn't get a sense that they are interacting. This is all trivial for real-world sports, because there's no artifice providing a view into the game system–the game system is a layer of pretense atop the physical universe, free of simulation.

We can look at agency in games as if we are having a conversation with the game. If you are talking to someone about elephants but they seem to respond regardless of your message with some mathematical equations about the shape of bananas, you wouldn't recognize that as a conversation. You are saying one thing, and independent of what you said, the other conversant said something else. You may be able to contrive a relationship, but it's far from obvious and intuitive. The person you're talking to may wait for a gap in your exposition to insert his irrelevant statements, which may convince you that your opposite is aiming for conversation, but that still leaves us entirely unsure you're having a conversation. In a game, you provide some input to the game and the game shows you a continuous stream of output. If the output doesn't seem relevant to your input, the connection between you and the game is not obviously there, and you are left with the impression that your input is ignored, much as a conversant spouting random facts at random intervals is, at best, questionably participating in a conversation. Establishing this feedback loop of relevance and reaction allows the player or conversant to build a causal model of the game or conversation in her mind that will map her actions to certain kinds of results based on observable contingencies. When Mary talked to Paul about politics, Paul got very agitated, so now Mary has this relationship between Paul, politics, and agitation in her mind. She’ll remember this the next time she tries to have a conversation with Paul and potentially use it to inform her communication with him. When you're playing Call of Duty and you click the left mouse button in the course of normal play your character's weapon appears to fire and the object your reticle is on seems to react visibly and audibly as if it were shot–now you can draw a causal relationship between that input and the effect on the game world.

Humans can be overwhelmed with contingencies and be rendered unable to draw any causal links. Humans can also draw causal links based on special cases that clearly are not representative, then, due to cognitive biases, ignore or disregard feedback that would show these highly-contingent causal links to be incorrect
