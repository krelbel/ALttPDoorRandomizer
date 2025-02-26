# ALttPDoorRandomizer

This is a door randomizer for _The Legend of Zelda: A Link to the Past_ for the SNES
based on the Entrance Randomizer found at [KevinCathcart's Github Project.](https://github.com/KevinCathcart/ALttPEntranceRandomizer)
See https://alttpr.com/ for more details on the normal randomizer.

# Documentation
1. [Setup and Installation](#setup-and-installation)
2. [Commonly Missed Things](#commonly-missed-things)  (** **Read This If New** **)
3. [Settings](#settings)
   1. [Dungeon Randomization](#dungeon-settings)
      1. [Dungeon Door Shuffle](#door-shuffle---doorshuffle)
      2. [Intensity Level](#intensity---intensity-number)
      3. [Key Drop Shuffle (Legacy)](#key-drop-shuffle-legacy---keydropshuffle)
      4. [Pottery](#pottery)
      5. [Shuffle Enemy Key Drops](#shuffle-enemy-key-drops---dropshuffle)
      6. [Experimental Features](#experimental-features)
      7. [Crossed Dungeon Specific Settings](#crossed-dungeon-specific-settings)
   2. [Item Randomization Changes](#item-randomization)
      1. [New "Items"](#new-items)
      2. [Shopsanity](#shopsanity)
      3. [Logic Level](#logic-level)
      4. [Goal](#goal)
      5. [Item Sorting](#item-sorting)
      6. [Forbidden Boss Items](#forbidden-boss-items)
   3. [Entrance Randomization](#entrance-randomization)
      1. [Shuffle Links House](#shuffle-links-house)
      2. [Overworld Map](#overworld-map)
   4. [Enemizer](#enemizer)
   5. [Game Options](#game-options)
   6. [Generation Setup & Miscellaneous](#generation-setup--miscellaneous)

## Setup and Installation

### Feedback and Bug Reports

Please just DM me on discord for now. I (Aerinon) can be found at the [ALTTP Randomizer discord](https://discordapp.com/invite/alttprandomizer).

### Installation

Click on 

https://github.com/aerinon/ALttPDoorRandomizer/releases

Go down to Assets and find a build for your system (Windows, Mac, or Linux)

Download and unzip. Find the DungeonRandomizer.exe or equivalent

### Installation from source

See these instructions.

https://github.com/aerinon/ALttPDoorRandomizer/blob/DoorDev/docs/BUILDING.md

When installing platform specific dependencies, don't forget to run the appropriate command from the bottom of the page! Those will install missing pip dependencies.

Running the MultiServer and MultiClient for multiworld should run resources/ci/common/local_install.py for those dependencies as well.

To use the CLI, run ```DungeonRandomizer.py```.

Alternatively, run ```Gui.py``` for a simple graphical user interface.

# Commonly Missed Things 
#### and Differences from other Randomizers

Most of these apply only when the door shuffle is not vanilla.

### Starting Item

You start with a “Mirror Scroll”, a dumbed-down mirror that only works in dungeons, not the overworld and can’t erase blocks like the Mirror.

### Navigation

* The Pinball Room’s trap door can be removed in the case where it is required to go through to get to the back of Skull Woods.
* Holes in Mire Torches Top and Mire Torches Bottom fall through to rooms below (you only need fire to get the chest)
* You can Hookshot from the left Mire wooden Bridge to the right one.
* In the PoD Arena, you can bonk with Boots between the two blue crystal barriers against the ladder to reach the Arena Bridge chest and door. (Bomb Jump also possible but not in logic - Boots are required)
* Flooded Rooms in Swamp can be traversed backward and may be required.

### Other Logic

* The chest in southeast Skull Woods that is traditionally a guaranteed Small Key in ER is not guaranteed here.
* Fire Rod is not in logic for dark rooms. (Hard enough to figure out which dark room you are in.) This is different from Advanced mode on the VT randomizer. Otherwise Advanced logic is always used. (There is no basic logic.)
* The hammerjump (and some other skips) are not in logic by default (see the mixed_travel setting for details). Doing so in a crossed dungeon seed can put you into another dungeon with the wrong dungeon id. (Much like EG)

### Boss Differences

* You have to find the attic floor and bomb it open and bring the maiden to the light to fight Blind. In cross dungeon door shuffle, the attic can be in any dungeon. If you bring the maiden to the boss arena, she will hint were the cracked floor can be found. If hints are on, there is a special one about the cracked floor.
* GT Bosses do not respawn after killing them in this mode.
* Enemizer change: The attic/maiden sequence is now active and required when Blind is the boss of Theives' Town even when bosses are shuffled.

### Crystal Switches

* You can hit the PoD crystal switch in the Sexy Statue room with a bomb from the balcony above without jumping down.
* GT Crystal Conveyor room (it has gibdos) - You can hit the crystal switch with a bomb when the blue barrier is up from the far side so you can leave the room to the left with blue barriers down.
* PoD Arena Bridge. If entering from the bridge, you can circle round and hit the switch, then fall into the hole to respawn at the bridge again with the crystal barriers different (if you don’t have a proper ranged weapon that can hit it)

### Misc

* Compass counts no longer function after you get the Triforce (this is actually true in all randomizers)

# Settings

## Dungeon Settings

Only extra settings are found here. All entrance randomizer settings are supported. See their [readme](https://github.com/KevinCathcart/ALttPEntranceRandomizer/blob/master/README.md)

### Door Shuffle (--doorShuffle)

* Vanilla - Doors are not shuffled
* Basic - Doors are shuffled only within a single dungeon.
* Crossed - Doors are shuffled between dungeons as well.

### Intensity (--intensity number)

* Level 1 - Normal door and spiral staircases are shuffled
* Level 2 - Same as Level 1 plus open edges and both types of straight staircases are shuffled.
* Level 3 -  Same as Level 2 plus Dungeon Lobbies are shuffled

### Key Drop Shuffle (Legacy) (--keydropshuffle)

Adds 33 new locations to the randomization pool. The 32 small keys found under pots and dropped by enemies and the Big
Key drop location are added to the pool. The keys normally found there are added to the item pool. Retro adds
32 generic keys to the pool instead. This has been can be controlled more granularly with the [Pottery](#pottery) and 
[Shuffle Enemy Key Drops](#shuffle-enemy-key-drops---dropshuffle) 

### Pottery

New pottery option that control which pots (and large blocks) are in the locations pool:

* None: No pots are in the pool, like normal randomizer
* Key Pots: The pots that have keys are in the pool. This is about half of the old keydropshuffle option
* Cave Pots: The pots that are not found in dungeons are in the pool. (Includes the large block in Spike Cave). Does
  not include key pots.
* Cave + Keys Pots: Both non-dungeon pots and pots that used to have keys are in the pool.
* Reduced Dungeon Pots: Same as Cave+Keys but also roughly a quarter of dungeon pots are added to the location pool picked at random. This is a dynamic mode so pots in the pool will be colored. Pots out of the pool will have vanilla contents.
* Clustered Dungeon Pots: Like reduced but pots are grouped by logical sets and roughly 50% of pots are chosen from those groups. This is a dynamic mode like the above.
* Excludes Empty Pots: All pots that had some sort of objects under them are chosen to be in the location pool. This excludes most large blocks and some pots out of dungeons.
* Dungeon Pots: The pots that are in dungeons are in the pool. (Includes serveral large blocks)
* Lottery: All pots and large blocks are in the pool.

By default, switches remain in their vanilla location (unless you turn on the legacy option below)

CLI `--pottery <option>` from `none, keys, cave, cavekeys, reduced, clustered, nonempty, dungeon, lottery`

Note for multiworld: due to the design of the pottery lottery, only 256 items for other players can be under pots in your world.

#### Colorize Pots

If the pottery mode is dynamic, this option is forced to be on (clustered and reduced). It is allowed to be on in all other pottery modes. Exceptions include "none" where no pots would be colored, and "lottery" where all pots would be. This option colors the pots differently that have been chosen to be part of the location pool. If not specified, you are expected to remember the pottery setting you chose. Note that Mystery will colorize all pots if lottery is chosen randomly.

CLI `--colorizepots`

#### Pot Shuffle (Legacy)

This continues to works the same by shuffling all pots on a supertile. It works with the lottery option as well to move the switches to any valid pot on the supertile regardless of the pots chosen in the pottery mode. This may increase the number of pot locations slightly depending on the mode.

### Shuffle Enemy Key Drops (--dropshuffle)

Enemies that drop keys can have their drop shuffled into the pool. This is the one part of the keydropshuffle option.
See the pottery option for more options involving pots.

### Experimental Features

You will start as a bunny if your spawn point is in the dark world. CLI: `--experimental`

### Crossed Dungeon Specific Settings

#### Dungeon Chest Counters

* Auto - picks an appropriate setting based on other settings. Generally will be pickup if the number of item in a dungeon changes.
* On - Dungeon counters on hud always displayed
* Off - Dungeon counters on hud never displayer
* On Compass Pickup - Dungeons with a compass item will display the counter once the compass is found. Dungeons without a compass item will display always unless the number of items in the dungeon is completely vanilla.

CLI: `--dungeon_counters` from `auto, on, off, pickup`

#### Mixed Travel (--mixed_travel value)

Due to Hammerjump, Hovering in PoD Arena, and the Mire Big Key Chest bomb jump, two sections of a supertile that are
otherwise unconnected logically can be reached using these glitches. To prevent the player from unintentionally changing
dungeons while doing these tricks, you may use one of the following options:

* Prevent (default): 
Rails are added the 3 spots to prevent these tricks. This setting is recommend for those learning crossed dungeon mode to learn what is dangerous and what is not. No logic seeds ignore this setting.
* Allow: The rooms are left alone and it is up to the discretion of the player whether to use these tricks or not.
* Force: The two disjointed sections are forced to be in the same dungeon but the glitches are never logically required to complete that game.

#### Standardize Palettes (--standardize_palettes)
No effect if door shuffle is not on crossed

* Standardize (default): Rooms in the same dungeon have their palettes changed to match. Hyrule Castle is split between Sewer and HC palette.
Rooms adjacent to sanctuary get their coloring to match the Sanctuary's original palette.
* Original: Rooms/supertiles keep their original palettes.

## Item Randomization

### New "Items"

#### Bombbag (--bombbag)

Two bomb bags are added to the item pool (They look like +10 Capacity upgrades). Bombs are unable to be used until one is found. Bomb capacity upgrades are otherwise unavailable.

#### Pseudo Boots (--pseudoboots)

Dashing is allowed without the boots item however doors and certain rocks remain un-openable until boots are found. Items that require boots are still unattainable. Specific sequence breaks like hovering and water-walking are not allowed until boots are found. Bonk distance is shortened to prevent certain pits from being crossed. Finding boots restores all normal behavior.

### Shopsanity

This adds 32 shop locations (9 more in retro) to the general location pool.

Multi-world supported. Thanks go to Pepper and CaitSith2 for figuring out several items related to this major feature.

Shop locations:
* Lake Hylia Cave Shop (3 items)
* Kakariko Village Shop (3 items)
* Potion Shop (3 new items)
* Paradox Cave Shop (3 items)
* Capacity Upgrade Fairy (2 items)
* Dark Lake Hylia Shop (3 items)
* Curiosity/Red Shield Shop (3 items)
* Dark Lumberjack Shop (3 items)
* Dark Potion Shop (3 items)
* Village of Outcast Hammer Peg Shop (3 items)
* Dark Death Mountain Shop (3 items)

Item Pool changes: To accommodate the new locations, new items are added to the pool, as follows:

* 10 - Red Potion Refills
* 9 - Ten Bombs
* 4 - Small Hearts
* 4 - Blue Shields
* 1 - Red Shield
* 1 - Bee
* 1 - Ten Arrows
* 1 - Green Potion Refill
* 1 - Blue Potion Refill
* 1 - +5 Bomb Capacity
* 1 - +5 Arrow Capacity

1. Initially, 1 of each type of potion refill is shuffled to the shops. (the Capacity Fairy is excluded from this, see step 4). This ensures that potions can be bought somewhere.
2. The rest of the shop pool is shuffled with the rest of the item pool. 
3. At this time, only Ten Bombs, Ten Arrows, Capacity upgrades, Small Hearts, and the non-progressive shields can appear outside of shops. Any other shop items are replaced with rupees of various amounts. This is because of one reason: potion refills and the Bee are indistinguishable from Bottles with that item in them. Receiving those items without a bottle or empty bottle is essentially a nothing item but looks like a bottle. Note, the non-progressive Shields interact fine with Progressive Shields (you never get downgraded) but are usually also a nothing item most of the time.
4. The Capacity Fairy cannot sell Potion Refills because the graphics are incompatible. 300 Rupees will replace any potion refill that ends up there.
5. For capacity upgrades, if any shop sells capacity upgrades, then it will sell all seven of that type. Otherwise, if plain bombs or arrows are sold somewhere, then the other six capacity upgrades will be purchasable first at those locations and then replaced by the underlying ammo. If no suitable spot is found, then no more capacity upgrades will be available for that seed. (There is always one somewhere in the pool.)
6. Any shop item that is originally sold by shops can be bought indefinitely, but only the first purchase counts toward total checks on the credits screen & item counter. All other items can be bought only once.

All items in the general item pool may appear in shops. This includes normal progression items and dungeon items in the appropriate keysanity settings.

#### Pricing Guide

#### Sphere effects

Design goal: Shops in early spheres may be discounted below the base price while shops in later spheres will likely exceed the base price range. This is an attempt to balance out the rupees in the item pool vs. the prices the shops charges. Poorer item pools like Triforce Hunt may have early shop prices be adjusted downward while rupee rich item pools will have prices increased, but later in the game.

Detailed explanation: It is calculated how much money is available in the item pool and various rupee sources. If this amount exceeds the total amount of money needed for shop prices for items, then shops that are not in sphere 1 will raise their prices by a calculated amount to help balance out the money. Conversely, if the amount is below the money needed, then shops in sphere 1 will be discounted by a calculated amount to help ensure everything is purchase-able with minimal grinding.

#### Base prices

All prices range approx. from half the base price to twice the base price (as a max) in increments of 5, the exact price is chosen randomly within the range subject to adjustments by the sphere effects above.

| Category            | Items                                                                                                      | Base Price |   Typical Range   |
|---------------------|------------------------------------------------------------------------------------------------------------|:----------:|:-----------------:|
| Major Progression   | Hammer, Hookshot, Mirror, Ocarina, Boots, Somaria, Fire Rod, Ice Rod                                       |    250     |      125-500      |
|                     | Moon Pearl                                                                                                 |    200     |      100-400      |
|                     | Lamp, Progressive Bows, Gloves, & Swords                                                                   |    150     |      75-300       |
|                     | Triforce Piece                                                                                             |    100     |      50-200       |
| Medallions          | Bombos, Ether, Quake                                                                                       |    100     |      50-200       |
| Safety/Fetch        | Cape, Mushroom, Shovel, Powder, Bug Net, Byrna, Progressive Armor & Shields, Half Magic                    |     50     |      25-100       |
| Bottles			          | Empty Bottle or Bee Bottle                                                                                 |     50     |      25-100       |
| 			                 | Green Goo or Good Bee                                                                                      |     60     |      30-120       |
| 			                 | Red Goo or Fairy                                                                                           |     70     |      35-140       |
| 			                 | Blue Goo                                                                                                   |     80     |      40-160       |
| Health              | Heart Container                                                                                            |     40     |       20-80       |
|                     | Sanctuary Heart                                                                                            |     50     |      25-100       |
|                     | Piece of Heart                                                                                             |     10     |       5-20        |
| Dungeon             | Big Keys                                                                                                   |     60     |      30-120       |
|                     | Small Keys                                                                                                 |     40     |       20-80       |
|                     | Info Maps                                                                                                  |     20     |       10-40       |
|                     | Other Maps & Compasses                                                                                     |     10     |       5-20        |
| Rupees			           | Green                                                                                                      |    Free    |       Free        |
| 			                 | Blue                                                                                                       |     2      |        2-4        |
| 			                 | Red                                                                                                        |     10     |       5-20        |
| 			                 | Fifty                                                                                                      |     25     |       15-50       |
| 			                 | One Hundred                                                                                                |     50     |      25-100       |
| 			                 | Three Hundred                                                                                              |    150     |      75-300       |
| Ammo	               | Three Bombs                                                                                                |     15     |       10-30       |
| 			                 | Single Arrow                                                                                               |     3      |        3-6        |
| Original Shop Items | Other Ammo, Refills, Non-Progressive Shields, Capacity Upgrades, Small Hearts, Retro Quiver, Universal Key |  Original  | .5 - 2 * Original |

#### Rupee Balancing Algorithm

To prevent needed to grind for rupees to buy things in Sphere 1 and later, a money balancing algorithm has been developed to counteract the need for rupees. Basic logic: it assumes you buy nothing until you are blocked by a shop, a check that requires money, or blocked by Kiki. Then you must have enough to make all purchases. If not, any free rupees encountered may be swapped with higher denominations that have not been encountered. Ammo may also be swapped, if necessary.

(Checks that require money: Bottle Merchant, King Zora, Digging Game, Chest Game, Blacksmith, anything blocked by Kiki e.g. all of Palace of Darkness when ER is vanilla)

The Houlihan room is not in logic but the five dungeon rooms that provide rupees are. Pots with rupees, the arrow game, and all other gambling games are not counted for determining income.

Currently this is applied to seeds without shopsanity on so early money is slightly more likely if progression is on a check that requires money even if Shopsanity is not turned on. 

#### Retro and Shopsanity

9 new locations are added.

The four "Take Any" caves are converted into "Take Both" caves. Those and the old man cave are included in the shuffle. The sword is returned to the pool, and the 4 heart containers and 4 blue potion refills are also added to the general item pool. All items found in the retro caves are free to take once. Potion refills will disappear after use.

Arrow Capacity upgrades are now replaced by Rupees wherever it might end up.
 
The Ten Arrows and 5 randomly selected Small Hearts or Blue Shields are replaced by the quiver item (represented by the Single Arrow in game.) 5 Red Potion refills are replaced by the Universal small key. It is assured that at least one shop sells Universal Small Keys. The quiver may thus not be found in shops. The quiver and small keys retain their original base price, but may be discounted.

### Logic Level

Overworld Glitches is now supported.

CLI: `--logic owglitches`

### Goal

Trinity goal is now supported. Find one of 3 triforces to win. One is at pedestal. One is with Ganon. One is with Murahdahla who wants you to find 8 of 10 triforce pieces to complete.

### Item Sorting

The "Item Sorting" option or ```--algorithm``` has been updated with new placement algorithms. Older algorithms have been removed.

When referenced below, Major Items include all Y items, all A items, all equipment (swords, shields, & armor) and Heart Containers. Dungeon items are considered major if shuffled outside of dungeons. Bomb and arrows upgrades are Major if shopsanity is turned on. The arrow quiver and universal small keys are Major if retro is turned on. Triforce Pieces are Major if that is the goal, and the Bomb Bag is Major if that is enabled.

Here are the current fill options:

#### Balanced

This one stays the same as before and is recommended for the most random distribution of items.

#### Vanilla Fill

This fill attempts to place all items in their vanilla locations when possible. Obviously shuffling entrances or the dungeon interiors will often prevent items from being placed in their vanilla location. If the vanilla fill is not possible, then other locations are tried in sequence preferring "major" locations (see below), then heart piece locations, then the rest except for GT locations which are preferred last. Note the PoD small key that is normally found in the dark maze in vanilla is move to Harmless Hellway due to the placement algorithm limitation.

#### Major Location Restriction

This fill attempts to place major items in major locations. Major locations are where the major items are found in the vanilla game. This includes the spot next to Uncle in the Sewers, and the Boomerang chest in Hyrule Castle.

This location pool is expanded to where dungeon items are locations if those dungeon items are shuffled. The Capacity Fairy locations are included if Shopsanity is on. If retro is enabled in addition to shopsanity, then the Old Man Sword Cave and one location in each retro cave is included. Key drop locations can be included if small or big key shuffle is on. This gives a very good balance between overworld and underworld locations though the dungeons ones will be on bosses and in big chests generally. Seeds do become more linear but usually easier to figure out.

#### Dungeon Restriction

The fill attempts to place all major items in dungeons. It will overflow to the overworld if there are more items than locations (e.g. Triforce hunt.) This fill does attempt to run the GT trash fill when possible. Seeds are typically very linear but tend to be more difficult.

#### District Restriction

The world is divided up into different regions or districts. Each dungeon is its own district. The overworld consists of the following districts:

Light world:

* Kakariko (The main screen, blacksmith screen, and library/maze race screens)
* Northwest Hyrule (The lost woods and fortune teller screens all the way to the river west of the potion shop)
* Central Hyrule (Hyrule castle, Link's House, the marsh, and the haunted grove)
* Desert (From the thief to the main desert screen)
* Lake Hylia (Around the lake)
* Eastern Hyrule (The eastern wild, the potion shop, and Zora's Domain)
* Death Mountain

Dark world:

* East Dark World (The pyramid, Palace of darkness, and Catfish)
* South Dark World (The dark lake, swamp area, to the dig game)
* Northwest Dark World (Village of Outcasts, to the Dark Sanctuary and screens in between)
* The Mire
* Dark Death Mountain

These districts are chosen at random and then filled with major items. If a location is part of a chosen district, but there are no more major items to place, a single green rupee is placed in the extra to indicate that as a placeholder. All other single green rupees are changed to be a blue rupee in order to not give false positives.

In entrance shuffle, what is shuffled to the entrances is considered instead of where the interior was originally. For example, if Blind's Hut is shuffled to the Dam, then the 5 chests in Blind's Hut are part of Central Hyrule instead of Kakariko.

Note: Bombos Tablet, Lake Hylia Island, Bumper Cave Ledge, the Floating Island, Cave 45, the Graveyard Cave, Checkerboard Cave and Mimic Cave are considered part of the light world region rather than the dark world region you mirror from.

In multiworld, the districts chosen apply to all players.

#### CLI values:

```balanced, vanilla_fill, major_only, dungeon_only, district```

#### New Hints

Based on the district algorithm above (whether it is enabled or not,) new hints can appear about that district or dungeon. For each district and dungeon, it is evaluated whether it contains vital items and how many. If it has not any vital item, items then it moves onto useful items. Useful items are generally safeties or convenience items: shields, mails, half magic, bottles, medallions that aren't required, etc. If it contains none of those and is an overworld district, then it checks for a couple more things. First, if dungeons are shuffled, it looks to see if any are in the district, if so, one of those dungeons is picked for the hint. Then, if connectors are shuffled, it checks to see if you can get to unique region through a connector in that district. If none of the above apply, the district or dungeon is considered completely foolish.

### Forbidden Boss Items

You may now restrict the items that can appear on the boss, like the popular ambrosia preset does.

CLI: ```--restrict_boss_items <option>```

#### Options

* none: As before, the boss may have any item including any dungeon item that could occur there.
* mapcompass: ~~The map and compass are logically required to defeat a boss. This prevents both of those from appearing on the dungeon boss. Note that this does affect item placement logic and the placement algorithm as maps and compasses are considered as required items to beat a boss.~~ Currently bugged, not recommended for use.
* dungeon: Same as above but both small keys and bigs keys of the dungeon are not allowed on a boss. (Note: this does not affect universal keys as they are not dungeon-specific)

## Entrance Randomization

### Shuffle Links House

In certain ER shuffles, (not dungeonssimple or dungeonsfulls), you can now control whether Links House is shuffled or remains vanilla. Previously, inverted seeds had this behavior and would shuffle links house, but now if will only do so if this is specified. Now, also works for open modes, but links house is never shuffled in standard mode.

### Overworld Map

Option to move indicators on overworld map to reference dungeon location. The non-default options include indicators for Hyrule Castle, Agahnim's Tower, and Ganon's Tower.

* Default:  Status quo. Showing only the prize markers on the vanilla dungeon locations.
* Compass:
    The compass item controls whether the marker is moved to the dungeons locations. If you possess the compass but not the map, only a glowing X will be present regardless of dungeon prize type, if you only possess the map, the prizes will be shown in predicable locations at the bottom of the overworld map instead of the vanilla location. Light world dungeons on the light world map and dark world dungeons on the dark world map. If you posses both map and compass, then the prize of the dungeon and the location will be on the map.
* Map: The map item plays double duty in this mode and only possession of the map will show both prize and location of the dungeon. If you do not shuffle maps or the dungeon does not have a map, the information will be displayed without needing to find any items.

If you do not shuffle the compass or map outside of the dungeon, the non-shuffled items are not needed to display the information. If a dungeon does not have a map or compass, it is not needed for the information. Talking to the bomb shop or Sahasrahla furnishes you with complete information as well as map information.

CLI ```--overworld_map [default, compass, map]```

## Enemizer

### Boss Shuffle: Unique

At least one boss each of the prize bosses will be present guarding the prizes. GT bosses can be anything.

### Blind Note

If bosses are shuffled and Blind is chosen to be the boss of Thieves Town, then bombing the attic and delivering the maiden is still required.

## Game Options

### MSU Resume

Turns on msu resume support. Found on "Game Options" tab, the "Adjust/Patch" tab, or use the `--msu_resume` CLI option.

### Collection Rate

Display the collection rate unless the triforce piece counter is needed. If the game was generated as a mystery, then the total count is not displayed. `--collection_rate`

### Reduce Flashing

Accessibility option to reducing some flashing animations in the game. `--reduce_flashing`

### Shuffle Sound Effects (--shuffle_sfx)

Shuffles a large portion of the sounds effects. Can be used with the adjuster.

## Generation Setup & Miscellaneous

### Create BPS Patches

Create bps patch(es) instead of generating rom(s) for distribution. `--bps`

### Triforce Hunt Settings

A collection of settings to control the triforce piece pool for the CLI/Mystery

* --triforce_goal_min: Minimum number of pieces to collect to win
* --triforce_goal_max: Maximum number of pieces to collect to win
* --triforce_pool_min: Minimum number of pieces in item pool
* --triforce_pool_max: Maximum number of pieces in item pool
* --triforce_min_difference: Minimum difference between pool and goal to win

### Seed

Can be used to set a seed number to generate. Using the same seed with same settings on the same version of the entrance randomizer will always yield an identical output.

### Count

Use to batch generate multiple seeds with same settings. If a seed number is provided, it will be used for the first seed, then used to derive the next seed (i.e. generating 10 seeds with the same seed number given will produce the same 10 (different) roms each time).



