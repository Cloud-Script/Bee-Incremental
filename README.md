---

# Group Boosts

Make sure to change your group for Group Boosts to work.  
To do this, go into **GameInfo (ModuleScript)** and replace `GroupId` with your own.

<img width="217" height="98" alt="image" src="https://github.com/user-attachments/assets/c46a07f0-af66-45c3-91cd-f6d68b33f6b8" />

---

# Shop

---

## Gamepass

To configure gamepasses, go into **GamepassData (ModuleScript)**.

<img width="221" height="103" alt="image" src="https://github.com/user-attachments/assets/10d6c941-52ed-46b1-b6da-4aaec426598a" />

In this module, you can find their names and IDs. Replace all IDs with your own **Gamepass IDs**.

You can create gamepasses in your Roblox experience settings, and make sure to put them on sale.

<img width="341" height="449" alt="image" src="https://github.com/user-attachments/assets/87b5c43f-e599-4c91-a7da-9748bf581973" />

---

## Product

To configure products, go into **ProductData (ModuleScript)** (same folder as GamepassData).

Change all products to your own (ProductData + GlobalRunes_1, Tickets, etc.).

<img width="190" height="67" alt="image" src="https://github.com/user-attachments/assets/550954b8-0f0f-427b-aa3e-73cbd6f6ff9e" />

In this module, you can find their names and IDs. Replace all IDs with your own **Product IDs**.

You can create developer products in your Roblox experience settings, and make sure to put them on sale.

<img width="341" height="449" alt="image" src="https://github.com/user-attachments/assets/15518065-d293-4f51-8e41-35dd1bdc240c" />

---

## Codes

To add codes, go into the **Codes (ModuleScript)**.

<img width="187" height="71" alt="image" src="https://github.com/user-attachments/assets/ee764e34-e051-4dfb-bd3f-fd088c34cf7b" />

You can add as many as you like. Simply copy an existing one, paste it, and change the name and rewards.

**Reward names:**
- `"Ticket"`, `"Honey"`, `"Stinger"`

---

# Game Configuration

Most of the game configuration is located in **Data (folder)** and **Game (model)** in Workspace.

<img width="208" height="82" alt="image" src="https://github.com/user-attachments/assets/ddcc4406-c255-44b3-8cdb-a9a208102fcb" />

---

## Icons
Each time you add a currency, rebirth, or similar item, make sure to add an icon in the `Icons` module.

<img width="182" height="93" alt="image" src="https://github.com/user-attachments/assets/c18dd98e-9b90-43e6-809f-6881c4bc9e2e" />

## GameInfo

In the `GameInfo` module, you can modify several values. Most names are self-explanatory, but here are some details:

- **DefaultSpawnTime**: A bee will spawn every X seconds (e.g., `1` = one bee per second). *(Default: 1)*  
- **DefaultMaxBee**: Maximum number of bees you can have. *(Default: 3)*  
- **DefaultStingerRarity**: Chance to obtain a stinger when collecting a bee.  
  Example: `100` = 1% chance *(Default: 100)*  
- **DefaultRange**: Default size of the range part. *(Default: 16)*  
- **DefaultRuneSpeed**: Time required to open a rune. *(Default: 1)*  

---

## Global Info

For most data, a **Type** system is used. Here are all available types:

- **Any Currency Name**: e.g. `"Honey"`, `"FrozenHoney"`  
- **Any Rebirth Name**: e.g. `"Rebirth"`, `"Prestige"`  

- **SpawnTime**: World-specific spawn time  
  Format: `"WorldNameSpawnTime"`  
  Example: `"World_1SpawnTime"`  

- **BeeLuck**: World-specific bee luck  
  Format: `"WorldNameBeeLuck"`  

- **MaxBee**: World-specific max bee limit  
  Format: `"WorldNameMaxBee"`  

- **StingerRarity**: Stinger drop luck  
  Example: `x2` = twice as many stingers  

- **Range**: Affects the range size  

- **RuneBulk**, **RuneLuck**, **RuneSpeed**, **RuneClone**: Rune-related stats  

---

## Upgrades

---

### Info

Each board has an invisible part inside **Game (model)**. This is where upgrades are displayed.  
The **name must match the Data module** (used for configuration below).

The part **must have the tag**: `"Upgrades"`.

<img width="240" height="94" alt="image" src="https://github.com/user-attachments/assets/ba7fd7c1-b8a5-419d-b5a9-96b18253feee" />

---

### Data Configuration

Find the module (must have the same name as the part displaying the upgrades).

<img width="234" height="108" alt="image" src="https://github.com/user-attachments/assets/04decc76-1fc5-4d97-8b44-87b8a8f43372" />

---

#### Visual

The first part of the module is for visuals:

- **Name**: Displayed at the top of the board  
- **Currency**: Currency used to purchase upgrades  
- **Limit**: Number of upgrades shown before overflow *(increase if needed)*  

Colors use gradients. You can also use `Color3.fromRGB` instead of `Color3.fromHex`.

- **Color**: Background frame  
- **InFrameColor**: Upgrade frame (slightly darker)  
- **TextColor**: Title text  
- **InTextColor**: Price/currency text  

---

#### Upgrade

You can add as many upgrades as you want. If they go out of the board, increase **Limit**.

Example:

```luau
RebirthMult = {
	Name = "Rebirth Mult",
	Icon = "rbxassetid://135657664642370",

	MaxLevel = 8,

	StartPrice = 1,
	PriceMult = 2.75,

	StartBoost = 1,
	Boost = 2,
	BoostType = "*",
	TotalBoost = "^",

	Type = "Rebirth",

	Display = "x",
	Order = 1,
},
```

--- 

**Understanding Boosts:**
There are 4 types of boosts and 1 special case:

**BoostType:**
- `"+"`: Adds the boost each level  
  Formula: `StartBoost + Boost * Level`
- `"-"`: Subtracts the boost each level  
  Formula: `StartBoost - Boost * Level`
- `"*"`: Multiplies the boost each level  
  Formula: `StartBoost * Boost * Level`
- `"/"`: Divides the boost each level  
  Formula: `StartBoost / Boost * Level`
  
**Special case:**
- **TotalBoost = "^"**: Enables exponential scaling (optional)  
  Add this line if you want exponential growth; otherwise, remove it.
  Formula:  
  `Value = StartBoost * (Boost ^ Level)`
  
> **Note:** The **Type** determines what the boost affects (see **## Global Info**).

--- 

**The price formula: (can be edited at the bottom of the upgrade module)**
```luau
math.floor(StartPrice * PriceMult ^ Level)
```

---

## Rebirth

---

Similar to upgrades, there is a part that displays the UI.  
**Tag:** `Rebirth`

---

### Configuration

---

The part **must have the same name as the module**:

<img width="235" height="110" alt="image" src="https://github.com/user-attachments/assets/c9ab3c3c-2ce7-4551-af32-915fe947728f" />

**Settings:**

- **Name**: Display name (recommended to match module script: `Rebirth`, `Prestige`, etc.)
- **Currency**: The currency used to buy the rebirth
- **Price**: Cost of one rebirth

**Colors:** Same as Upgrade Visual configuration

Reset:
The hardest part is what the rebirth resets. Example:

```luau
Reset = {
	{{"Honey"}, 0, "Set"},
	{{"Upgrades", "BeeUpgrades"}, {}, "Set"},
},
```
Explanation:
- PlayerData.Honey = 0 → Resets the player's honey
- PlayerData.Upgrades[BeeUpgrades] = {} → Removes all BeeUpgrade upgrades
- The "Set" action simply sets the value in PlayerData to the one defined in the reset table.
- You can add more entries to reset whatever else you want upon rebirth.

--- 

## Bee

TODO

---

## Runes

---

Similar to upgrades, there is a part that displays the UI.  
There is also a separate part for the button.  
**The module and the display/button parts must have the same name.**

<img width="155" height="87" alt="image" src="https://github.com/user-attachments/assets/10d1931b-4265-423a-8cdb-b2533d54c84e" />

---

### Configuration

---

Most settings are self-explanatory. Here are the key details:

- **Rarity**: Determines drop chance. Formula: `1 / Rarity`  
  Example: `Rarity = 10` → `1 / 10 = 10%` chance

- **Boosts**: Same as upgrade boosts.  
  You can define `BoostType`, `StartBoost`, `Boost`, and `TotalBoost` exactly like you do for upgrades.

---

---

## World

---

Here you can learn how to configure and add worlds.

---

### Zones

---

If you want to add a world, make sure the zone fits the world map.  
Each world has a zone, which is used to determine which world the player is in.

<img width="151" height="125" alt="image" src="https://github.com/user-attachments/assets/3a0e83fd-8343-431c-b5d5-96a9d6a84e10" />

---

### Bee Spawn Zones

---

Each world has a spawn part for bees.  
Simply clone it and resize if you want it larger.

<img width="147" height="81" alt="image" src="https://github.com/user-attachments/assets/3590a121-4622-47c8-b4cd-4b7355ca3f6b" />

---

### Portal

---

Portals are simple. Each portal has two parts: 

- **Hit** → The part the player touches  
- **To** → The destination part  

When the player touches `Hit`, they are teleported to `To` if they have access to the world.

---

### World Configuration

---

All world settings are in the world data modules.  
Everything is organized and easy to understand.  
If you want to add a new world, just follow the structure in the modules.

--- 

### Bee Worlds

--- 

TODO

---

# Tutorial

---

## Add Worlds

---

First, you need a map.  
For example, you can clone the **Snow Map** and edit its colors to create a Desert or Lava map.  

Move the cloned map **750 studs** along any axis (remember this number for later you can move by 2K studs for exemple I take 750).

<img width="819" height="412" alt="image" src="https://github.com/user-attachments/assets/84b4f85e-1001-4996-a4c7-dd3121cb3807" />

> At this point, nothing on the cloned map will work yet.

---

### Adding Portals

---

We already have a portal for World 3 (if not, just clone an old one):

1. Move the **To** part 1500 studs so it matches World 3's spawn.
2. Keep the **Hit** part in place.

<img width="192" height="133" alt="image" src="https://github.com/user-attachments/assets/5aecafbf-e2e8-4006-8817-555970244cfd" />
<img width="531" height="351" alt="image" src="https://github.com/user-attachments/assets/62b77c42-0a76-43f7-a592-bab0f12b56c2" />

---

### Creating a New Portal for Previous Worlds

---

To create a portal to go back to an old world:

1. Duplicate the portal that redirects to the previous world.  
   (If making World 3, clone **Portal World_1**)
2. Move it **750 studs**.
3. Rename it `"World_2"` to direct players to World 2.
4. Duplicate the portal decoration, move it, and update the **TextLabels** (There is 2, one is children of the other one):
   - Change `"World 1"` → `"World 2"`

---

### Configuring the World

---

TODO
