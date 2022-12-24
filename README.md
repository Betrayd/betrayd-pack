# Betrayd Pack

### The resource pack for the Betrayd Minecraft server.
Adds custom guns, sounds, cosmetics and more...

[![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/TZ5hdRrpDT)

## 🎨 Custom gun skin tutorial

**Requirements:**
- [Blockbench](https://www.blockbench.net/) or another Minecraft model editing program
- [Aseprite](https://www.aseprite.org/) or another image manipulation tool (Recommended)

### Step 0 - Best practices
This isn't so much a step but more of a list of things you should keep in mind when making gun skins
- Make entire skin packs rather than individual gun skins
- Index your PNGs (More detail in Step 2). The pack is already big and will get bigger over time so we want to save space where possible
- Keep your pack name short and simple
- Avoid [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) by painting overlapping surfaces the same colour. Sometimes you can do this by erasing some of the overlaping pixels on one of he cubes

Ignoring these steps will decrease the likeliness of your gun skins getting added.

### Step 1 - Getting the files
Download the gun model and texture of the gun you want to skin.
Model | Texture
------|---------
[pistol/basic.json](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/models/gun/pistol/basic.json) | [pistol/basic.png](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/textures/gun/pistol/basic.png)
[revolver/basic.json](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/models/gun/revolver/basic.json) | [revolver/basic.png](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/textures/gun/revolver/basic.png) 
[rifle/basic.json](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/models/gun/rifle/basic.json) | [rifle/basic.png](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/textures/gun/rifle/basic.png)
[shotgun/basic.json](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/models/gun/shotgun/basic.json) | [shotgun/basic.png](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/textures/gun/shotgun/basic.png)
[sniper/basic.json](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/models/gun/sniper/basic.json) | [sniper/basic.png](https://github.com/yo314159at/betrayd-pack/tree/main/assets/minecraft/textures/gun/sniper/basic.png)

It is recomended to save the files as `<gun type>.json`/`<gun type>.png` in order to avoid confusion between the basics

⚠️ *If you want a detailed gun skin and you downloaded `basic.png` you will have to scale it up. (An image size of 128x128 is recommended for pixel consistency with the rest of the gun skins). Alternatively you can download another gun skin that is already scaled up from the same directory*

### Step 2 - Making the texture
Open the model in a model editing program and apply the texture. (The following steps apply only to Blockbench)
- In the home screen press `Open Model`
- Navigate to the JSON file and open it
- Right-click the missing texture and press `Change file`
> ![change file](https://user-images.githubusercontent.com/51864749/208269731-8c09ca88-fb4b-402d-af09-ad2287aad23d.png)
- Navigate to the PNG file and open it
- Navigate to the `Paint` tab and use Blockbench's built in tools **OR** Open the texture in an image manipulation tool and edit the texture there, when saving Blockbench will update the 3D preview (Desktop only!) ⚠️ **DO NOT change the model of the gun, only the texture!**
- Once you're done making your gun skin, if you edited it using Blockbench, press the save icon in the textures list to update the file (Or save the new texture in the web version)
> ![paint](https://user-images.githubusercontent.com/51864749/208269932-b28578a4-617c-43ec-9c48-6fb7a34b4fef.png)
- **HIGHLY ENCOURAGED!** Change the colour mode of the texture to `Indexed` in Aseprite this is done via `Sprite > Color Mode > Indexed`, this saves up a lot of storage space. When indexing your texture **make sure** all of the colours have remained consistant, if indexing causes an error in the colours you do not know how to fix you should undo and keep the texture in the default `RGB Color` mode.

If you don't know how/want to use Git you can send the textures you made in the [Discord server](https://discord.gg/TZ5hdRrpDT) so someone else can update the pack for you, then skip to [Step 4](.#step-4---the-end). Otherwise lets continue...

### Step 3 - Updating the pack
Lets add your brand new gun skins to the resource pack so they could work in-game.
- Clone this repository
- Choose a name for your gun skin pack
- Add the gun skins in the directory `/assets/minecraft/textures/gun/<gun type>/<pack name>.png`
- Create a new JSON file called `<pack name>.json` in the directory `/assets/minecraft/models/gun/<gun type>/`:
```json
{
	"parent": "gun/<gun type>/basic",
	"textures": {
		"0": "gun/<gun type>/<pack name>"
	}
}
```
- Create another JSON file called `<pack name>.json` in the directory `/assets/minecraft/models/gun/<gun type>/aiming/`:
```json
{
	"parent": "gun/<gun type>/aiming/basic",
	"textures": {
		"0": "gun/<gun type>/<pack name>"
	}
}
```
- Find your pack's index by referencing this table:

Pack name | Index
----------|-------
Basic     | 1
Cosmic    | 3
Camo      | 5
Your pack | 7
- Add your pack's index to the gun's base model ID to get the custom model data of the gun

Gun      | Base model ID
---------|---------------
Pistol   | 0
Revolver | 10,000
Rifle    | 20,000
Sniper   | 30,000
Shotgun  | 40,000
- Add your models to `/assets/minecraft/models/item/feather.json`'s overrides
```json
{
  ...,
  "overrides": [
    ...,
    {"predicate": {"custom_model_data":<gun's custom model data>}, "model": "gun/<gun type>/<pack name>"},
    {"predicate": {"custom_model_data":<gun's custom model data + 1>}, "model": "gun/<gun type>/aiming/<pack name>"}
  ]
}

```
- Edit the pack index reference table starting at line 76 in `README.md` (Hey that's here!)
```md
...

Pack name   | Index
------------|-------
Basic       | 1
...         | ...
<pack name> | <your index>
Your pack   | <your index + 2>

...
```
- Create a pull request

### Step 4 - The end
Congratulations, You've made a weapon skin pack! 

Please note that we might not add every single skin for various reasons and we do not owe you an explination if we choose to decline it. If your skin is accepted, once your pull request is resolved (or someone updates the pack for you if you're joining us from Step 2) it means that your gun skins will be added in the next update.

Please do not bother Betrayd staff about when you will see your guns in the game; even after they are in the pack the gun skins still need to be implemented in the code with flavour text and loot crates. (Feel free to suggest the former as part of the pull request or in Discord)
