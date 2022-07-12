# Player attributes

In SimpleMMO, each character is described by three main stats: strength (str); defence (def); and dexterity (dex). During combat, the two combating characters' stats are compared in a series of calculations. The game then rolls for damage dealt based on the outcome of these calculations. Additionally, dex alone is used to determine the chance of completing a quest. Stats can be boosted by leveling up, purchasing gear, and having a job with a stat bonus.


## Combat Mechanics
### Definitions
- Player A has total stats (stra, defa, dexa)
- Player B has total stats (strb, defb, dexb)
- Maxab() is the maximum damage player A can deal to player B
- Minab() is the minimum damage player A can deal to player B
- CtHab() is the chance player A has to hit player B
### Functions
- Maxab(stra, defb) = str_a - (9/11)*defb
In practice, this function is rounded to the nearest whole number and floored at 20
- Minab(stra, defb) = str_a - (11/9)*defb
In practice, this function is rounded to the nearest whole number and floored at 1
- CtHab(dexa, defb) = (7/2)*(dexa / defb)
This is CtH as a probability between 0 and 1. Though CtH() can return values higher than 1, the game counts all CtH() ≥ 1 as a hit.
### Turns
SimpleMMO's combat is turn-based. Every turn, each character attacks the other exactly once. Damage is dealt to both characters simultaneously. For each character each turn, the game rolls against CtH() to see if the attack lands, then rolls a number between Min() and Max() to determine damage dealt.

### Critical/Special Attack
The attacking player has an option to special attack. This consumes one energy, and boosts the player's str stat for one turn. The boost is +25% by default, but can be raised with crit boosting gear. The crit bonus is applied to the str stat before any of the above calculations are performed.
