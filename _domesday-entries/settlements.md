---
layout: page
title: Settlements
section: basics
---

# Overview

Settlements are the population centers on the Kingdom Mode map. Taking control of settlements is central to  the Kingdom Mode because settlements are the only source for **Population** and **Food**.

---

## Taking Control

Settlements can begin the game as **Neutral** or controlled by a dynasty.

* A dynasty can take control of a settlement with the **Siege** action. Additionally, **Neutral** settlements can be 'peacefully' taken over with the **Annex** action.

* When a character completes a succesful **Siege** or **Annex** action they become the new Lord of the settlement.

### Prestige and Honor Gain

#### Dynasty Prestige

* Dynasties earn 100 **Prestige** for each settlement they control at the beginning of the month

#### Lord of the Settlement

* The Lord of a settlement gains 100 **Honor** at the start of every month.

---

## Growth

Settlement population growth occurs once a day. Growth is calculated by a formula that considers current population, max population and several variables.

#### Population/Max Ratio

> Population/Max Ratio: (TotalPopulation / PopulationLimit) * 100

#### Base Growth (determined from Pop/Max Ratio)

>| Ratio  | Value  |
>|:-:|:-:|
>| 0-10  | .1  |
>| 11-20  | .09 |
>| 21-30  | .088  |
>| 31-55  | .086  |
>| 56-77  | .08  |
>| 78-100  | .06  |

#### Bonus Growth

>| Ratio  | Value  |
>|:-:|:-:|
>| 0-100  | .02  |

#### Actual Growth

> Actual Growth = **BaseGrowth** * (100 - **PopMaxRatio**) * **BonusGrowth**

#### Growth from Cottage Workers (for each Cottage)

>CottageModifiedGrowth = **ActualGrowth** + ((Workers/2) * .1)

#### Manor Efficiency Bonus

>ManorModifiedGrowth = ManorWorkers * .1 * **CottageModifiedGrowth**

#### Unrest modifier

Lastly, Growth is modified by the unrest of the settlement. Unrest is a value between 0 and 100

>FinalGrowth = (100 - UnrestLevel / 100) * **ManorModifiedGrowth**

---

## Farming

The farming cycle occurs in three phases: Planting, Harvesting, and Winter

### Planting

A settlement will plant food equal to the number of available Farmers modified by a scalar

> BaseFoodPlanted = NumberOfFarmers * 5

#### Manor Efficiency Bonus

>FinalFoodPlanted = ManorWorkers * .1 * **BaseFoodPlanted**

### Harvesting

During the harvest months (March, October) farmers extract the planted food and store it in the settlement

> BaseFoodHarvested = NumberOfFarmers * 10

#### Manor Efficiency Bonus

>FinalFoodHarvested = ManorWorkers * .1 * **BaseFoodHarvested**

### Winter

During the winter months Farmers get a break! Use them to build things, or put them in an army to get ready for the spring campaign

---

## Trade

Trade daily occurs when a settlement has at least one Market

#### Trade from Markers (for each Market)

> BaseTradeCoin = NumberOfWorkers * 1

#### Manor Efficiency Bonus

>FinalFoodHarvested = ManorWorkers * .1 * **BaseTradeCoin**

<!-- <span style="color:blue"> blue text</span> -->