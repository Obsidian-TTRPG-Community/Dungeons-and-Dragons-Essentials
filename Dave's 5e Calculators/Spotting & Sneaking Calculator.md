---
title: Spotting & Sneaking Calculator
aliases: 
category: Tool
type: Calculator
sizeFactor: 1
hearing: 3.9229213002324457
weather: 1
invisibilityMod: 3.0778623055634844
func: 0.7845842600464892
spotter: "[[6. Mechanics/CLI/bestiary/humanoid/goblin.md|goblin]]"
sneaker: "[[6. Mechanics/CLI/bestiary/legendary-group/white-dragon.md|white-dragon]]"
spotterPerc: 10
sneakerPerc: 12
terrain: 15
wind: 1
light: 3
rain: 1
size: 0
spyglass: false
darkvision: false
metric: 1
invisibility: false
penalties: 1
penaltyFactor: 3.3333333333333335
---

#  Spotting & Sneaking Calculator

> [!infobox | left wfull]
> # `INPUT[suggester(optionQuery(#monster OR #PC OR #NPC)):spotter]` Spotting `INPUT[suggester(optionQuery(#monster OR #PC OR #NPC)):sneaker]`
> # Spotter Perception: `INPUT[number(class(nb-mb-35)):spotterPerc]` Sneaker Stealth: `INPUT[number(class(nb-mb-35)):sneakerPerc]`
> || 
> |-|-|
> Terrain |  `INPUT[inlineSelect(option(2, Arctic), option(2.5, Desert), option(5.00003, Farmlands), option(15, Forest), option(5.00001, Grasslands), option(10.00002, Hills), option(20, Jungle), option(5.00002, Meadows), option(15.00001, Mountains), option(0.2, Open Sea), option(2.00001, Sea During Storms), option(0.5, Sea Near Coast), option(15, Steep Mountains), option(22.5, Strange cosmology), option(15.00002, Swamp), option(30, Underground)):terrain]`
> Wind | `INPUT[inlineSelect(option(1, Calm-Fresh Breeze), option(1.33333, Strong Breeze-Gale), option(2, Strong Gale-Violent Storm)):wind]`
> Light |  `INPUT[inlineSelect(option(1, Bright), option(2, Dim Light/Lighty Obscured), option(3, Darkness/Heavily Obscured)):light]` 
> Precipitation | `INPUT[inlineSelect(option(1, Clear-Light), option(2, Moderate-Substantial), option(4, Heavy-Very Heavy)):rain]`
> Object size | `INPUT[inlineSelect(option(-3, Fine), option(-2, Tiny), option(-1, Small), option(0, Medium), option(1, Large), option(2, Huge), option(3, Gargantuan), option(4, Colossal)):size]`
> # Options
> ||
> -|-|-|-
> Spyglass? | `INPUT[toggle():spyglass]` | Invisible? | `INPUT[toggle():invisibility]`
> Darkvision? |  `INPUT[toggle():darkvision]`|  Metric? | `INPUT[toggle(offValue(1), onValue(0.3048)):metric]`
> # Spot Distance: `VIEW[min(round({light} == 3 & not({darkvision}) ? {hearing}*{func}*{metric} : {invisibility} ? {invisibilityMod} : 5000/{terrain}*{weather}*{sizeFactor}*{func}*{metric}), 30000*{metric})]` `VIEW[{metric} < 1 ? "m" : "ft"]`
>> [!note | clean no-t]-
>> Size factor: `VIEW[pow(exp(log(2)*({size}+{spyglass})), 2)][math():sizeFactor]`
>> Hearing modifier: `VIEW[{light} == 3 & not({darkvision}) ? 5*{func}*pow((1/({wind}*{rain}))*exp(log(2)*{size}), 3) : 1][math():hearing]` 
>> Weather: `VIEW[({light}-{darkvision} == 2 ? sqrt(0.1) : 1)*(1/{rain})*(1/{wind})][math():weather]`
>> Terrain: `VIEW[1/{terrain}]`
>> Invisibility: `VIEW[(1/{rain})*(1/{wind})*5*{func}*pow((1/({wind}*{rain}))*exp(log(2)*{size}), 3)*{func}*{metric}][:invisibilityMod]`
>> Func: `VIEW[max(1.002876172*2*(1/(1+exp(0.2181959805*({sneakerPerc}-{spotterPerc})))-1/(1+exp(30*0.2181959805))), 0)][math():func]`
^SpottingCalculator
