## WIP - This page is being actively developed

Parts of this page may or may not apply to menus, but this page focuses on the controlbar buttons and textures that are presented to the player ingame and pertain mostly to the resolution scaling & positioning behavior.

The results and findings on this page are based on the tests using only the 2560x1440 resolution.

This game uses a single commandbar texture and a single scheme (per faction) to dynamically scale across several screen resolutions. It does not work very well for resolutions above the officially supported which do not include widescreen aspect ratios.

Instead of trying to figure out how the existing scaling system works in practice, it is simply easier for Thyme to implement, simpler to maintain and more practical to create the necessary textures and configs for each of the established resolutions separately.


### **ControlBarScheme.ini**

- ScreenCreationRes: Doesn't really work as it sounds. It affects the positioning and scaling, making it very tied to the resolution of the texture even tho the whole point of dynamic scaling is to have one universal texture that can be adjusted internally. There seems to be an additional problem with width issue where texture gets cutt off at higher width, which requires the use of a wider canvas size of the texture (with alpha layer).


### **ControlBar.wnd**


