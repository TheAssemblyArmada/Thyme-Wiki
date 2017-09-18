## WIP - This page is being actively developed

Parts of this page may or may not apply to menus, but this page focuses on the controlbar buttons and textures that are presented to the player ingame and pertain mostly to the resolution scaling & positioning behavior.

The results and findings on this page are based on the tests using only the 2560x1440 resolution.

This game uses a single commandbar texture and a single scheme (per faction) to dynamically scale across several screen resolutions. It does not work very well for resolutions above the officially supported which do not include widescreen aspect ratios.




### **ControlBarScheme.ini:**



- ScreenCreationRes: Doesn't really work as it sounds. It affects the positioning and scaling, making it very tied to the resolution of the texture even tho the whole point of dynamic scaling is to have one universal texture that can be adjusted internally. There seems to be an additional problem with width issue where texture gets cutt off at higher width, which requires the use of a wider canvas size of the texture (with alpha layer).

- Y Parameter: Changing this one in any way from the default 600 will put the whole controlbar texture out of bottom screen alignment, therefore it is useless.

- X Parameter: 

- This affects the s?controllbar.tga texture that is on one of the layers, it also affects the scaling of generals powers and other textures for some weird reason, it does not control the scale and positioning of the button controls and their elements.

- Because it scales the controlbar's buttons, but not command buttons, it does have an effect on alignment of a lot of other things not just the texture, it is important to note that the controlbar's parent scaling is DIFFERENT from the controllbar texture, when the controlbar's parent is in the proper position, the texture will most probably not be scaled correctly, in order to fix this it is required to finetune the texture it self, unfortunately.

- Most of the time has to be spent on finetuning at the texture level, editing the .tga to get the scaling/positioning just right, a very inefficient way of doing things.



### **ControlBar.wnd:**



***

### **Proposed Solution:**

Instead of trying to figure out how the existing scaling system works in code, it is simply easier for Thyme to implement, and simpler to maintain as well as more practical to create the necessary textures and configs for each of the established resolutions separately.

- Remove the scaling system, each resolution uses it's own scheme and window settings.

- Reimplement the behavior of these parameters, so they can be easily adjusted with a calculation or automation to create other resolution configs without manually tediously finetuning the the positioning for each one.

- Remove the secondary scaler for the s?controlbar.tga texture, and reimplement it so that it will work 1:1 with the source texture on disk. For example, for the 2560x1440 screen resolution, the source texture would be exactly the same at 2560x1440. However, the actual controlbar would only be an area at the bottom of this texture, and the rest would be an empty canvas area with a fully transparent alpha channel, that would be equal to the battlefield camera area in-game, this also gives the modder/maintainer great preview as to how it would look like in-game in practice directly from the photo editor. The engine would then simply load the texture as centered on the screen without any need to adjust any scaling or position parameters and fully independent of any other component of the GUI.

