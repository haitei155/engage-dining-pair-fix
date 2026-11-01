# Fire Emblem Engage — Custom Unit Support

[简体中文](README.md)

**v0.3** · Expanded skill-inheritance lists, paired-dining dialogue fallback and six-frame PNG Loading dots.

**Install [Cobalt](https://github.com/Raytwo/Cobalt) first.** Thank you to **Raytwo** for developing and maintaining Cobalt and providing the mod-loading foundation used by this project.

The current binary targets Fire Emblem Engage 2.0.0 with Cobalt 1.31.0 as its compatibility baseline.

## Download and Installation

**[Download the complete v0.3 package: engage_custom_unit_support.zip](https://github.com/haitei155/engage-custom-unit-support/releases/download/v0.3/engage_custom_unit_support.zip)** · [Release page](https://github.com/haitei155/engage-custom-unit-support/releases/tag/v0.3) · [SHA256SUMS](https://github.com/haitei155/engage-custom-unit-support/releases/download/v0.3/SHA256SUMS)

The complete ZIP contains `engage_custom_unit_support.nro` and three UI resource files: `godinfo.bundle`, `unitselectroot.bundle` and `skillselectroot.bundle`. No separate downloads are needed. The Bundles extend the original interface with expanded controls and layouts. They work alongside the NRO, which provides the plugin logic. **Installing or replacing only the NRO does not provide the v0.3 UI capacity expansion.**

1. Install the prerequisite runtime following [Cobalt](https://github.com/Raytwo/Cobalt)'s instructions, then fully exit the game.
2. Choose one method: place the complete ZIP unchanged in `engage/mods/`, or extract all its contents into `engage/mods/engage-custom-unit-support/`, preserving the internal `Data/` directory structure. Do not install both the ZIP and an extracted copy.
3. When upgrading, replace the complete plugin package. For an extracted installation, update both the NRO and the three Bundles under `Data/`. **Remove the old `engage_dining_pair_fix.nro`** to avoid duplicate hooks. If a mod collection already includes this plugin, use that copy without a separate installation.
4. Fully restart the game. Emulators use their configured virtual SD card directory; returning to the title screen is not a full restart.

An extracted installation has the following layout; with the ZIP method, these files remain inside the ZIP:

```text
engage/mods/engage-custom-unit-support/
├─ engage_custom_unit_support.nro
├─ Data/StreamingAssets/aa/Switch/fe_assets_ui/hub/godroom/prefabs/
│  ├─ godinfo.bundle
│  ├─ unitselectroot.bundle
│  └─ skillselectroot.bundle
└─ RELEASE_NOTES.md
```

The separate NRO on the Release page contains only the plugin program and does not replace the complete installation package. Six-frame Loading PNGs are supplied separately by character packages; they are not part of these three UI Bundles. See below for their format and filenames.

## New in v0.3

### Expanded skill-inheritance lists

With added emblems, the bond-level panel on the unit-selection screen can run out of entries, and moving past the 20th emblem in the inheritance details can freeze the menu. The two screens have separate limits: 19 display entries and 20 navigation indicators.

v0.3 expands the bond-level panel to **22 entries in two columns and 11 rows**, adds the corresponding background row, extends the panel down near the bottom of the screen, and increases row height to give the text more space. If more than 22 emblems are owned, this panel displays at most 22 entries.

The inheritance details provide **30 navigation slots**. Native sorting, left/right navigation and wraparound remain in use. The indicator row scales to two thirds of its original size to accommodate 30 slots. Lists beyond 30 require further UI resource expansion. Only owned emblems appear; the plugin does not grant rings, skills or bond levels.

Install the NRO and all three UI resource files from the complete package; see Download and Installation above for filenames and paths. Controls are expanded in the resources and initialized by the native flow; the NRO adds a navigation bounds guard. Fully restart the game after updating.

**UI resource rights notice:** these three Bundles, including copies in the complete ZIP, are excluded from the plugin code's Apache-2.0 license. Their rights are described separately in the [UI resource rights notice](resources/inheritance/NOTICE.md).

## v0.2 Features

### Six-frame Loading dots

When native Loading setup cannot find a character texture, this plugin reads the actual converted UnitIconID from enabled Cobalt packages. Preferred resource: `patches/icon/loading/Dot_Run_<UnitIconID>.png` — a transparent **288×48 RGBA PNG containing six 48×48 frames in one horizontal row**, with matching spelling and case. This is one sprite sheet; GIFs and six separate files are not runtime inputs. A corresponding Loading Bundle remains a fallback when no usable PNG is present. Missing or invalid resources are skipped.

**MOD creators must make their own six-frame Loading PNGs.** This plugin provides resource loading and native animation support; it does not create the artwork. The supplied Lumera example was made by the project author. Other characters still require their MOD creators to make the corresponding sprite sheets.

#### Lumera PNG example

![Lumera — six horizontal Loading run frames](images/lumera-loading-run-six-frames.png)

Example file: [`lumera-loading-run-six-frames.png`](images/lumera-loading-run-six-frames.png). This author-made Lumera Loading animation uses a transparent **288×48 RGBA PNG**, with six **48×48** frames arranged horizontally. MOD creators can use it as a reference for the sprite-sheet format and resource setup.

To use it in Lumera's character package, rename the downloaded example to `Dot_Run_555Lumiere.png` and place it at `patches/icon/loading/Dot_Run_555Lumiere.png`. The example's descriptive filename is for documentation; the runtime filename must match Lumera's actual UnitIconID, `555Lumiere`. For another character, supply that character's own six-frame sheet with the matching key. The NRO does not generate missing artwork.

The native game still chooses the Loading mode, invitation participants or sortie roster, and drives the six-frame animation. Loading screens without the native dot queue do not gain a forced queue. The v0.2 implementation restores a retained material template before clearing a custom slot, protects cached textures against Unity asset unloading, and reloads an invalid cache entry. These changes address white squares on subsequent Loading screens.

The standard build does not emit plugin diagnostic logs. Resources are cached during a game session; editing a PNG or ZIP requires a full game restart.

## v0.1 Features

### Paired dining

- Provides a fallback for paired-dining combinations without a dedicated conversation label.
- Only an empty label triggers the original meal-evaluation helper, selecting good/normal/bad reactions according to the character, dish quality and preferences.
- Existing valid paired-dining labels are retained.

### Dining scenes

The screenshot below shows the opening scene of a paired meal involving a custom added character. In the author's tests, affected pairs frequently freeze after this scene when the patch is absent. Some pairs lack a dedicated conversation label; the original flow receives an empty label and cannot continue normally. This patch falls back to the native meal-evaluation dialogue selection at that point.

![Paired-dining opening scene: affected pairs may freeze after this scene](images/paired-dining-opening-before-dialogue.jpg)

With the patch enabled, the following screenshots show this pair continuing into normal meal-evaluation dialogue. Support notifications shown here belong to the normal game flow. The patch prevents a missing conversation label from blocking the meal; it does not create extra support events.

![Alear's meal-evaluation dialogue continues after the fix](images/paired-dining-dialogue-alear.jpg)

![Eirika's meal-evaluation dialogue continues after the fix](images/paired-dining-dialogue-eirika.jpg)

## Upgrading from the previous project name

Previously named `engage-dining-pair-fix`, this project is now `engage-custom-unit-support`. The v0.2 NRO is `engage_custom_unit_support.nro`. It includes the original dining fix; installing both NRO names creates duplicate hooks. Replace the old NRO when upgrading.

## Source and Build

See [Build instructions](docs/BUILD.md). The source includes skill-inheritance list expansion, paired-dining fallback, Loading resource support and their local dependencies. Builds go to `dist/`; `Releases/` contains the v0.3 binary and its checksum.

## License and Credits

| Content | License or rights notice |
|---|---|
| Project-owned code, modification scripts and documentation | [Apache License 2.0](LICENSE) |
| Three companion UI Bundles, including copies in the complete ZIP | [UI resource rights notice](resources/inheritance/NOTICE.md); excluded from the code license above |
| Third-party dependencies and upstream-derived portions | Their respective terms; see [THIRD_PARTY.md](THIRD_PARTY.md) and [NOTICE](NOTICE) |

The complete installation package contains content with different licensing scopes; the ZIP as a whole is not uniformly licensed under Apache-2.0.

Thanks to [Raytwo](https://github.com/Raytwo/Cobalt), [skyline-rs](https://github.com/skyline-rs) and all relevant dependency contributors.
