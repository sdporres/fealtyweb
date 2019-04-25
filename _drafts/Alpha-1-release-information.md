---
layout: post
title: Alpha 1 is getting pretty damn close
---

Well, people, I have been writing lots of code for about a month. Almost exactly a month, actually - the first commit was 24 March 2019. Over the past month the project has achieved a very important milestone - it is playable! Like, holy shit, its hideous and ugly, but there is a *nugget* of an experience here!

Allright, so what is going to be in this release?

## Alpha 1 - The Kingdom Game

The most basic-playable-thing I could start off with is the Kingdom Game. 
```
The "Kingdom Game" is the primary game mode in Fealty - it is where your characters do things and develop, and the vehicle for your Dynasty to gain Prestige.
```
In the next few weeks leading up to the release I will go into more detail about the design of elements in the Kingdom Game, but here is a summary of what you can do in Alpha 1.

## Settlements

Settlements are important because controlling them is the primary way of gaining Power. 
```
Power is important because it converts into Prestige at the end of the game.
```

### Food and Population
Settlements are sole source of Food and Population in the game, both of which which are needed to take control over enemy settlements.
```
Food is grown by your Population - but Population is also the source of Troops for your Characters. You have to balance aggression with planning.
```

### Buildings
Every settlement has a Manor, which acts as the HQ of the settlement. In addition, players can construct Cottages and Markets.
```
* Cottage   - increases population limit
* Market    - can assign Population to produce Coin
```

## Characters
Characters execute your will in the Kingdom Game. They can lead Troops to Siege and Attack your enemies.

### Actions
In this alpha we have a basic set of actions characters can perform with settlements and other characters.

```
* Move      - travel to an adjance settlement
* Annex     - attempt to convince a Neutral settlement to join you
* Siege     - attempt to starve an enemy settlement into submission
* Attack    - attempt a battle with an enemy character to kill them, or force them to retreat

There are other actions which a character does not start willingly, like Retreat.
```

---

Now that we have gone over the concept and our design goals, we are turning our full attention to the Kingdom Game. Next time we will talk about the Kingdom Game prototype design, and our roadmap for the near future.

-FealtyDev

![FealtyDevPortrait](/public/images/fealtydevportrait.jpeg){: .portrait }