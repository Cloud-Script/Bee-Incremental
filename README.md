# Animation

---

We cannot make the collecting animation public.  
If you want to use it, you need to upload the animation to Roblox and copy its ID.

<img width="418" height="496" alt="image" src="https://github.com/user-attachments/assets/e602be3b-4cfa-4409-9e45-9b93d5561144" />

Then, replace the animation ID in the **CollectBee** properties with your own.

<img width="232" height="194" alt="image" src="https://github.com/user-attachments/assets/08fd2302-36c1-49c5-9409-3c42a88a91ea" />

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
	...
},
```

Explanation:
- PlayerData.Honey = 0 → Resets the player's honey
- PlayerData.Upgrades[BeeUpgrades] = {} → Removes all BeeUpgrade upgrades
- The "Set" action simply sets the value in PlayerData to the one defined in the reset table.
- You can add more entries to reset whatever else you want upon rebirth.

---

## Bee

---

To configure bees, go into the **BeeData module** of the world you want to edit.

<img width="217" height="107" alt="image" src="https://github.com/user-attachments/assets/0dbb0ffd-c6e8-4348-8c86-485b3ab7483e" />

---

### Configuration

- **Currency**: The name of the currency the bee gives  
- **DropColor**: The color of the drop *(e.g. blue for a frozen world)*  
- **DropTrail**: The color of the trail *(same idea as DropColor)*  

---

### Bee Settings

Each bee has its own configuration:
- **Model**: The model path  
  Example:  
  `BeeAssets.World_1.Angel`  
  *(BeeAssets = ReplicatedStorage.Assets.Bee)*  

<img width="193" height="110" alt="image" src="https://github.com/user-attachments/assets/763ad858-0243-4bcf-88e0-da0b1389c882" />

- **Rarity**: Works the same as rune rarity  
  Formula: `1 / Rarity`  
  *(See Runes configuration for more details)*  

- **StingerRarity**: Increases the chance to drop a stinger  
  Formula: `DefaultChance / StingerRarity`  

- **Stats**: The amount of currency the bee gives  

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

## World

---

Here you can learn how to configure worlds.

---

### Zones + Spawn

---

If you want to add a world, make sure the zone fits the world map.  
Each world has a zone, which is used to determine which world the player is in.

<img width="151" height="125" alt="image" src="https://github.com/user-attachments/assets/3a0e83fd-8343-431c-b5d5-96a9d6a84e10" />


---

### Player Spawn

---

You also need a spawn location for the player.

Place a spawn point in your world, then add it to the **LocationData** module.

<img width="163" height="86" alt="image" src="https://github.com/user-attachments/assets/a343bb29-6a52-4317-b6cd-f3a1d590e548" />

<img width="215" height="129" alt="image" src="https://github.com/user-attachments/assets/bda07e3b-827e-4525-9bab-123df7827607" />

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

Each world has its own bee.  
See **Bee Configuration** for more information.

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

3. Make sure the pivot is in front of the model (This is where the UI will show on Portal World 3 it wasn't so just put it in fonrt of the model (Moving it by 755 stud should be good!

<img width="452" height="322" alt="image" src="https://github.com/user-attachments/assets/b6cd28c1-f12e-4598-bfda-531890b81e7d" />

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

#### Add to Worlds

---

In the **WorldData** module, you can add a new world (e.g. World 3).

You can edit the price and other settings. In this example, we simply copied **World_2** and changed the name and values.  
*(See World Configuration above for more details)*

<img width="190" height="96" alt="image" src="https://github.com/user-attachments/assets/5e5151a8-9556-42e3-97af-71f705e69db0" />

---

### Final Script Example

```luau
return {
    CanTeleport = {
        World_1 = true,
    },

    World_2 = {
        Display = "World 2",
        Currency = "Honey",
        Price = 1000000,
    },
    
    World_3 = {
        Display = "World 3",
        Currency = "FrozenHoney",
        Price = 1000000,
    },
}
```

After this, players will be able to purchase and access World 3.

---

#### Zones + Spawn Zones + Spawn

---

- First, clone the **World_2** zone and move it (e.g. 750 studs).  
- Resize it if you're using your own map and it's bigger.  
- Rename it to **World_3**  

<img width="174" height="93" alt="image" src="https://github.com/user-attachments/assets/91c731c9-f1a6-4b8b-bffe-843891da3c0b" />

- Do the same for the **bee spawn zone**  

<img width="166" height="108" alt="image" src="https://github.com/user-attachments/assets/e8647118-750e-4f19-afba-ca98f87a2680" />

Make sure to also add a **World_3 player spawn**  
*(See World Configuration → Player Spawn above)*

---

#### Adding Bees

---

If you try to play after adding the zone, the game will not work because no bees can spawn in **World_3**.

To fix this, simply clone the **World_2 BeeData** and rename it to **World_3**.

<img width="136" height="88" alt="image" src="https://github.com/user-attachments/assets/0b749613-687e-4b4d-84ad-db1ae5f8fc3d" />

Make sure to change the currency, unless you want it to be an extension of another world.
Make sure to also add the currency icon in the **Icons** module.
(See **Configuration → Icons** above if needed.)
Example:
```luau
Currency = "LavaHoney",
```

You can then edit the file:
- Add more bees  
- Change models  
- Rename bees  

*(See Bee Configuration if needed)*

---

#### ⚠️ IMPORTANT (OR IT WILL NOT WORK)

The top UI is **not dynamic** — it is pre-made.  
So you must create a UI for your new currency.

Go into **HUD**, duplicate an existing UI, then:
- Change its color
- Rename it to match your currency  

*(Icons are set dynamically, so you don’t need to change the icon manually.)*

<img width="293" height="240" alt="image" src="https://github.com/user-attachments/assets/0b4e5aa6-e8dc-4718-8981-840b636b5241" />

---

#### Upgrades

Now bees can spawn... but there are no upgrades yet.

- Clone the invisible part used for the upgrade board  
- Rename it to something **unique**  
  Example: `World_3BeeUpgrades`

<img width="222" height="211" alt="image" src="https://github.com/user-attachments/assets/85b97287-07e2-4a99-a3b6-da5a63a56629" />
<img width="877" height="359" alt="image" src="https://github.com/user-attachments/assets/d0013ce9-1eff-4688-97af-57838f2dc7fd" />

Then:
- Clone the corresponding module script  
- Rename it to match (e.g. `World_3BeeUpgrades`)  

Configure the file:
- Set the correct **currency**
- Update upgrade types if needed *(see Upgrade Configuration)*  

⚠️ Important:
- Replace all `World_2` references with `World_3`  
- Example: `World_2SpawnTime` → `World_3SpawnTime`  
- Use **Ctrl + F** in the script editor to replace everything  

Repeat this for each upgrade board in your new world.

---

#### Rebirth

Same process as upgrades:

- Duplicate the invisible part  
- Rename it (example: `Ascension`)  

<img width="163" height="86" alt="image" src="https://github.com/user-attachments/assets/c39b5d6d-7bd6-4079-9570-470684a9032b" />

Then:
- Duplicate the module script  
- Rename it to match  
- Change the currency and configuration if needed  

---

#### Runes

Same as upgrades/rebirth, but with an extra button:

- Clone the invisible display part **and** the button  
- Rename both to `World_3`

<img width="158" height="159" alt="image" src="https://github.com/user-attachments/assets/3a1f0b6c-e344-4280-a2c6-b9448b08a7eb" />

- Clone the module script and rename it `World_3`

<img width="168" height="108" alt="image" src="https://github.com/user-attachments/assets/4f00adc5-4c72-4a08-9237-58e1ce950e93" />

Then configure:
- Change the **name**
- Replace `"FrozenHoney"` with your new currency  
- Adjust boosts if needed *(see Runes Configuration)*  

Example (top of the file):

<img width="809" height="144" alt="image" src="https://github.com/user-attachments/assets/0b29577b-8fab-4337-adfa-ca5a9560c827" />

⚠️ Important:
- Replace all `World_2` references with `World_3`  
- (Use **Ctrl + F**)
- Also, I noticed a problem in the UI: for all world displays, **delete** the `UIAspectRatioConstraint` in the Template.  
- <img width="351" height="320" alt="image" src="https://github.com/user-attachments/assets/97636531-cdd8-468a-8c48-f7fbd503b95f" />



---

#### Others

- Duplicate all **gamepass boards** and move them (e.g. 750 studs)

<img width="323" height="292" alt="image" src="https://github.com/user-attachments/assets/57c11cb5-39c9-4fcc-a78b-ed8d3cdf5572" />

- Check **leaderboard configuration** if you want to add stats for your new currency
- If you cloned the Snow map, you can remove the clicker, add a new functionality with your own script, or simply remove it completely.
- And I hope I didn't forget anything
