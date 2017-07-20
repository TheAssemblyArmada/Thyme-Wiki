You've found a bug, made your way to the issue tracker and are ready to report it... but what exactly do you need to report? Well, at a bare minimum you will need a description of what the bug is, something along the lines of "Sound isn't working" or "Graphics are messed up". Well, that tells us there is a problem, but what we really need is a...

#### Detailed Description

A detailed description includes a description of what isn't working and the circumstances in which it doesn't work. For our examples you might have the following:

"Sound isn't working for when I click on units, but the music is playing in game so I know its producing some sound."

"Graphics are messed up, where there are supposed to be roads there are just purple strips."

Both of these give some indication of what specifically we are looking for and what should happen when the bug is fixed. However, what if the bug was something that only happened under circumstances? Something like "I can make the scud storm fire continuously" reports a bug, but to fix it we need to know how its caused. We need...

#### Steps to Reproduce

No, this doesn't mean we want something like the Karma Sutra, it means we need a set of instructions to make the bug happen so we can look at what code is being used when it happens and we can test that any fixes we make actually stop it. [How to do the Scud Bug](http://www.wikihow.com/Do-the-Scud-Bug-in-C%26C-Generals-or-Zero-Hour) is a good example of steps to reproduce a bug. What if it only happens with certain content though, such as customized ini files or a map? Then you need...

#### Test Data

Test data is just data that the developers might not have to hand. If you've made a custom map for example and the bug only manifests there. It may well be that its an error in the custom content or it could just be that the custom content is using an obscure function in the engine that isn't well tested. To be sure you would have to include it in the report, either attached or uploaded somewhere and linked to. There is also one more thing you might want to include in your report given that Thyme is a reimplementation of another game...

#### Happens in Vanilla

Does the bug happen in the original game? If it does, that doesn't mean we won't try and fix it in Thyme, but at least we know Thyme in and of itself isn't the cause of it. There is also the possibility that its outside the scope of Thyme to fix. As a rough guide, if a mod to the original game can fix the bug, its probably not something that Thyme needs to fix as it likely isn't an engine bug, its a configuration bug.