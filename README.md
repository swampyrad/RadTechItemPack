# Radtech Item Pack

A collection of various items for [Hideous Destructor](https://codeberg.org/mc776/HideousDestructor). Includes various medical items, wearables and more.

## Field-Medic Kit

* **Actor Class**: `HDFieldMedicKit`
* **Loadout Code**: `fmd`
  * An emergency medical kit that contains rolls of medical gauze, tape, scissors and more to help speed up the bandaging process of bleeding wounds. A bit more sanitary and safe, though that usually doesn't cross many soldier's minds when they need to use one.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/fieldmedickit.png)

### Field-Medic Kit Settings

* **Spawn Bias**: `fieldmedic_stimpack_bias` - How common the Field Medic Kit will spawn on stimpacks. Lower is more common.
  * `19` = Default Spawn Chance
* **Spawn Bias**: `fieldmedic_medikit_bias` - How common the Field Medic Kit will spawn on medikits. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `fieldmedic_persistent_spawning` - If the Field Medic Kit can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Field-Medic Kit Controls

* **Fire**: Use on yourself
* **Alt. Fire**: Use on someone else
* **Alt. Reload**: Remove blood feeder (if any)

## Leather Armour

* **Actor Class**: `HDLeatherArmour`
* **Loadout Code**: `awl | arl`
  * Mostly known nowadays as the "Poor Mans Garrison Armour", many scavengers and civilians will create and wear these as a replacement for proper armor until they find some. Due to usually being weaved with Kevlar, this bit of leather armour will still save your life from a couple pistol shots, though higher rounds or dangers will still get through.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/leatherarmor.png)

### Leather Armour Settings

* **Spawn Bias**: `jacketarmour_spawn_bias` - How common the Leather Jacket will spawn on Armour. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `jacketarmour_persistent_spawning` - If the Leather Jacket can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Leather Armour Controls

* **Use Item**: Wear
* **Strip Armor**: Take off

## Anti-Gravity Boots

* **Actor Class**: `AntiGravBoots`
* **Loadout Code**: `agv`
  * Similar to the Anti-Radiation Boots, but painted in cherry red. These boots allow the wearer to lower their gravity to jump across large gaps, or get into hard-to-reach areas. Features an internal charging system powered by the ambient frag flying all over the place, so you never have to worry about keeping batteries handy.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/antigravboots.png)

### Anti-Gravity Boots Settings

* **Spawn Bias**: `gravboots_spawn_bias` - How common pairs of Anti-Gravity boots spawn with Soulspheres. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `gravboots_persistent_spawning` - If pairs of Anti-Gravity boots can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Anti-Gravity Boots Controls

* **Use Item**: Wear
* **Strip Armor**: Take off

## Anti-Radiation Boots

* **Actor Class**: `ProtectiveRadBoots`
* **Loadout Code**: `rdb`
  * A pair of boots designed with use in nuclear testing sites and cleanup zones for nuclear waste. It'll protect your feet against any radioactive threats, though the rest of your body may not be too happy with it.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/antiradboots.png)

### Anti-rad boot Settings

* **Spawn Bias**: `radboots_spawn_bias` - How common pairs of Anti-Radiation boots spawn with Radsuits. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `radboots_persistent_spawning` - If pairs of Anti-Radiation boots can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Anti-rad boot Controls

* **Use Item**: Wear
* **Strip Armor**: Take off

## Radi-cola

* **Actor Class**: `HDRadicola`
* **Loadout Code**: `rdc`
  * An energy drink commonly found in the fridges and convenience stores of the civilian world, though recently taken completely off shelves due to supposed radiation and stimpack poisoning found inside of the cans. Drink with caution.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/radicola.png)

### Radi-cola Settings

* **Spawn Bias**: `radicola_healthbonus_bias` - How common Radi-cola spawns instead of Health Bonuses. Lower is more common.
  * `19` = Default Spawn Chance
* **Spawn Bias**: `radicola_stimpack_bias` - How common Radi-cola spawns instead of Stimpacks. Lower is more common.
  * `19` = Default Spawn Chance
* **Spawn Bias**: `radicola_medikit_bias` - How common Radi-cola spawns on medikits. Lower is more common.
  * `19` = Default Spawn Chance
* **Spawn Bias**: `radicola_gorebits_bias` - How common Radi-cola spawns on. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `radicola_persistent_spawning` - If Radi-cola can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Radi-cola Controls

* **Fire**: Use on yourself
* **Alt. Fire**: Use on someone else

## Halfpack

* **Actor Class**: `HDHalfPack`
* **Loadout Code**: `hpk`
  * A smaller form of the usual standard issue backpack, originally intended for use with civilians but it later saw some use before the invasion by soldiers not needing to hold as many magazines due to the weight decreases from use of the Volt ZM-66.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/halfpack.png)

### Halfpack Settings

* **Spawn Bias**: `halfpack_spawn_bias` - How common the M-211 Sigcow spawns on Clip Boxes. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `halfpack_persistent_spawning` - If the M-211 Sigcow can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### Halfpack Controls

* **Fire/Alt. Fire**: Previous/Next Item
* **Zoom + Fire/Alt. Fire**: Cycle mag
* **Firemode + Mouselook**: Scroll through items
* **Reload**: Insert item
* **Unload**: Remove item
* **Drop One**: Remove and drop
* **Alt. Reload**: Dump contents of bag

## First-Aid Medical Spray

* **Actor Class**: `HDFirstAidSpray`
* **Loadout Code**: `aid`
  * An experimental can of second-flesh medical solution, made for treating burns and helping quicken the healing process for flesh wounds. These were eventually replaced with the Second-Flesh applicators we know and see today due to their improved capacity and scanning functionality, though these'll get the job done in a pinch.

![Thumbnail](https://github.com/Gay-Snake-Squad/RTWP-ImageHosting/blob/main/Screenshots/firstaidspray.png)

### First-Aid Spray Settings

* **Spawn Bias**: `firstaidspray_stimpack_bias` - How common First Aid Spray will spawn on stimpacks. Lower is more common.
  * `19` = Default Spawn Chance
* **Spawn Bias**: `firstaidspray_medikit_bias` - How common First Aid Spray will spawn on medikits. Lower is more common.
  * `19` = Default Spawn Chance
* **Persistent Spawning**: `firstaidspray_persistent_spawning` - If containers of First Aid Spray can spawn after mapload.
  * `False` = Default Value
  * `True` = Enables persistency for spawning

### First-Aid Spray Controls

* **Reload**: Take off armor
* **Fire**: Use on yourself
* **Alt. Fire**: Use on someone else
  * ...while pressing:
  * **Nothing**: Treat wounds
  * **Zoom**: Treat burns

## Radi-radio

* **Actor Class**: `HDFieldMedicKit`
* **Loadout Code**: `prd`
  * An old emergency radio originally used to communicate with other people, though can now still be used to play local music files. Convenient, especially since helmet music functionality has been made irrelevant since the invasion.

### Radi-radio Controls

* **Fire**: Switch to next channel
* **Alt. Fire**: Switch to previous channel
* **Turn off radio**: Unload
