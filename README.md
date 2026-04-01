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


