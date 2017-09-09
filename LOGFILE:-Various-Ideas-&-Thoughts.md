## WIP - This page is under active development - contents may change completely

***

This page is meant for more informal and initial mentioning of ideas and thoughts that aren't serious enough or the person just didn't develop it on it's own to be able to fully explain and present a case for it. These mostly wouldn't be part of Thyme in any way but are interesting nontheless to have an overview of the stance/reasoning the community have in mind sorrounding Generals Zero Hour. Some of the things discussed here might turn out to be substantial enough and will be escalated to the Enhancements List.

***
**GLOSSARY:**

* IUAI: Internal Unit Artificial Intelligence (such as `Retaliation`)
* Prop: Proposition

***
***
***

# **Various Ideas**

## **Controllability**
* Ability to adjust location of the offmap cargo plane spawnpoint for caputrable tech buildings (Ai should also be able to do this)

## **Gameplay Logic**
* Ability to reverse the cargo loading procedure - Instead of the unit to be loaded moving to the transporter, the unit stands still and the transporter comes to it.

## **Problematic Units**
### Tactical Nuke MiG 
* Behaviors and components that aircraft use are already problemating, combining that with the Tactial Nuke warhead upgrade, it makes the Nuke MiG stand out from all the rest as the most problematic aircraft unit.
* Experiences frequent friendly fire.
* REFs -> GuardArea behavior, many keep target dead flying unit air bounce, range + flying height, attack/move

## **Problematic Gameplay Behavior**
### Aircraft `GuardArea` Behavior - (ref -> Tactical Nuke MiG = TACMG)
* Case1: InsideGuardArea = Aircraft idling inside guard area waiting for enemies to enter zone
* Case2: EnrouteToGuardArea = Aircraft enroute to guard area with enemy presence
* Problem1: InsideGuardArea: Enemy aircraft that rush into the guard zone are able (major cause of friendly fire for TACMG)
* Problem2: EnrouteToGuardArea: Aircraft are not attacking the nearest enemy unit to the point from which they enter the guard area, even if it's attacking them.
* Prop1: increase the global nominal aircraft-flying-height defaults
* Prop2: increase the `GuardArea` radius size defaults
* Prop3: The aircraft IUAI should retaliate against the attacking unit even if the aircraft is guarding and the attacking unit is outside the guard area.
* Prop2: IUAI should determine 
* Prop3: IUAI should further

### Aircraft Unit-Not-Completely-Dead-Targeting Issue (ref -> Tactial Nuke MiG)
* Problem: WIP todo

***

### Aircraft Attack-Move Behavior Shortcomings
* Problem: Seems that they are skipping some targets, including the ones that are attacking them, ..

***

## **Specific _BehaviorModule_ Behavior Ideas**
* MODZ: Aircraft Guard Behavior 

***

## Battlefield GUI
* Flashing or static icon on aircraft without available hangar slot (the icon could be displayed static while aircraft is en-route by player command, has ammo, or is guarding, when it performs it's RTB command the icon will start flashing)
* Show Cargo Pips When Transporter Full Exception - Otherwise hidden unless selected (A Gameplay setting under Options Menu?)

***

## Battlefield Behavior
* Ability to multi-select structures (for training, multi-activate things like "overload power", but probably not upgrades) 

## System Info & Diagnostics
* Thyme should add a small non-annoying, barely noticable icon to some non-interesting part of the screen during gameplay to indicate that Thyme is active. Users watching various streams and recorded videos would know where to look for an be able to instantly know whether or not Thyme was used in the viewing video. This should help with chat spam and questions.

***
***
***

# **Thoughts & Questions**
* When reverse cargo loading behavior is implemented, should all transport units be given 2 control buttons necessary for choosing mode? If yes, which setting would be the default?
* Should infantry be very slowly healed when garrisoned in civilian buildings?
* Should China speaker towers be allowed to block line of sight to base defences? - not sure if they do that.
* Should deployable units when deployed undeploy and move out of the way when a unit paths through or should they ignore? Manual deployment?
* Is it really necessary for aircraft to start losing health when they are requesting a landing hangar slot, if they can guard indefinitely while armed why can't they idle without weapons - at least the rate could be lowered some? Would any change here really severely affect the balance and the originality?
* Should aircraft making a landing request be redirected to the nearest HQ position rather than the position of the airfield that they took off from? That position might still be under enemy presence. This redirection shoud happen as part of the RTB command that the unit-AI performs, which means as soon as it runs out of ammo, this should also nicely fit the timing when the flashing "no-hangar" icon is activated.
