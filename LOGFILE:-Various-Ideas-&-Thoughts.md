## WIP - This page is under active development - contents may change completely

***

This page is meant for more informal and initial mentioning of ideas and thoughts that aren't serious enough or the person just didn't develop it on it's own to be able to fully explain and present a case for it. These mostly wouldn't be part of Thyme in any way but are interesting nontheless to have an overview of the stance/reasoning the community have in mind sorrounding Generals Zero Hour. Some of the things discussed here might turn out to be substantial enough and will be escalated to the Enhancements List.

Items on this page are actively modified and deleted (strikethrough?).

# Various Ideas
## Controllability
* Ability to adjust location of the offmap cargo plane spawnpoint for caputrable tech buildings (Ai should also be able to do this)

## Gameplay Logic
* Ability to reverse the cargo loading procedure - Instead of the unit to be loaded moving to the transporter, the unit stands still and the transporter comes to it.

## Problematic Units
### Tactical Nuke MiG 
* guard behavior, friendly fire, civ buildings, ammo target dead unit, short range

## Problematic Gameplay Behavior
### WIP - Aircraft Guard Behavior, esp Tactical Nuke MiG 
* Proposition1: increase default global aircraft flying height
* Prop2:
* Prop3:

## Specific BehaviorModule Behavior
* TODO: Aircraft Guard Behavior 

## Battlefield GUI
* Flashing or static icon on aircraft without available hangar slot (the icon could be displayed static while aircraft is en-route by player command, has ammo, or is guarding, when it performs it's RTB command the icon will start flashing)
* Show Cargo Pips When Transporter Full Exception - Otherwise hidden unless selected (A Gameplay setting under Options Menu?)

## System Info & Diagnostics
* Thyme should add a small non-annoying, barely noticable icon to some non-interesting part of the screen during gameplay to indicate that Thyme is active. Users watching various streams and recorded videos would know where to look for an be able to instantly know whether or not Thyme was used in the viewing video. This should help with chat spam and questions.

# Thoughts & Questions
* When reverse cargo loading behavior is implemented, should all transport units be given 2 control buttons necessary for choosing mode? If yes, which setting would be the default?
* Should infantry be very slowly healed when garrisoned in civilian buildings?
* Should China speaker towers be allowed to block line of sight to base defences? - not sure if they do that.
* Should deployable units when deployed undeploy and move out of the way when a unit paths through or should they ignore? Manual deployment?
* Is it really necessary for aircraft to start losing health when they are idling for landing request, if they can guard while armed why should they - at least the rate could be lowered some?
* Should aircraft making a landing request be redirected to the nearest HQ position rather than the position of the airfield that they took off from? That position might still be under enemy presence. This redirection shoud happen as part of the RTB command that the unit-AI performs, which means as soon as it runs out of ammo, this should also nicely fit the timing when the flashing "no-hangar" icon is activated.
