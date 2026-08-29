# WoVR Quest Community Patch

## Version 1.0 — Initial Community Release

An unofficial community patch for **ProjectMimer's WoVR**, focused on improving World of Warcraft 3.3.5a VR functionality, comfort, Meta Quest controller support, and overall playability.

## 🎥 See WoVR in Action

Want to see WoVR running before installing it?

### 🏰 Tram Ride & Gryphon Flight — World of Warcraft in VR

▶️ [Watch the WoVR Tram Ride & Gryphon Flight Showcase](https://youtu.be/6FlpryqCXLo)

Take a ride through Azeroth in VR! This showcase features the Deeprun Tram between Ironforge and Stormwind followed by a gryphon flight back to Ironforge, demonstrating head tracking, smooth locomotion, VR UI interaction, and the overall immersion of experiencing World of Warcraft from inside the headset.

### ⚔️ WoVR Gameplay Showcase


▶️ [Watch the WoVR Gameplay Showcase](https://www.youtube.com/watch?v=wEPjaiBd0x8&t=14s)

See World of Warcraft 3.3.5a running in VR with first-person exploration, motion controls, UI and menu interaction, and combat.

### 💚 Support the Project

The **WoVR Quest Community Patch is completely free** and will remain freely available through GitHub.

If you'd like to support the time that goes into development, testing, troubleshooting, documentation, and future improvements:

☕ [Support Briinc3 on Ko-fi](https://ko-fi.com/briinc3)

Support is completely optional and is **not required to download or use the community patch.**

### 📥 Download

➡️ [Download the latest WoVR Quest Community Patch](https://github.com/Briinc3/WoVR-Quest-Community-Patch)

---
## Update - August, 29, 2026

Flat VR Interface — Reworked the WoW UI rendering surface from a curved segmented panel to a flat VR display for improved readability, consistency, and menu interaction.
+ Ability to switch back to the curved UI look if you wish. The current D3D9.dll file has the flat UI, while the D3D9_(curved UI).dll has the curved UI. To switch, all you need to do is remove the _(Curved ui) text from that dll, and rename the current one to _(Flat ui) and vise versa if you want to switch back. The mod reads whichever file says D3D9.dll, so you can choose which one you want to load in.

## Update - August, 26, 2026

Warmane: Tested and working with the Warmane 3.3.5a client. This does not imply endorsement or approval by Warmane. Use of client modifications is subject to the rules of the server you connect to.

## Update - August, 25, 2026

## ⚠️ Known Limitation — Nameplate Stereo Rendering

### Double Nameplates in VR

When enemy or friendly nameplates are enabled, WoVR may display what appears to be two slightly offset copies of the same nameplate.

This is a known visual limitation of the current build.

It does **not** affect targeting, combat, controller input, UI interaction, or normal gameplay.

### Why wasn't this simply fixed?

We spent approximately **24 working hours investigating this issue**, including extensive source-code testing, render logging, shader identification, texture tracing, per-eye rendering experiments, UI render-target testing, and testing with both Blizzard's default nameplates and 3.3.5a-compatible Tidy Plates.

During that investigation, we learned that WoW's nameplates behave differently from normal interface elements.

Nameplates are tied to the game's world/UI rendering system rather than behaving like ordinary static interface elements such as action bars, bags, or character windows.

WoVR then has to translate WoW's original DirectX 9 rendering into a stereoscopic VR image.

This creates an unusual situation:

- The 3D world is rendered separately for each eye.
- Much of WoW's interface is rendered through a shared UI path.
- Nameplates are visually attached to objects in the 3D world while also being handled through WoW's UI system.
- In VR, this can result in the nameplate appearing at slightly different positions between the two eye views.

Your brain therefore sees two offset nameplates instead of one perfectly fused plate.

### Why not just line the two nameplates up?

Unfortunately, the two images cannot simply be moved on top of each other.

Correct stereoscopic placement depends on several things, including:

- Left/right eye position
- Camera projection
- Head movement
- Distance from the player
- The position of the unit in the 3D world
- WoW's UI/world projection
- WoVR's stereo rendering pipeline

A fixed offset might make a nameplate line up at one particular distance or viewing angle, but it could become incorrect again as soon as the player moves their head, turns the camera, or the enemy changes distance.

A proper solution would therefore require changing how the nameplate is projected into VR rather than simply shifting one copy sideways.

### What we tried

During development we tested multiple approaches, including:

- Identifying nameplate-specific DirectX draw calls
- Comparing render logs with nameplates ON and OFF
- Tracking vertex and pixel shader hashes
- Tracking texture dimensions and texture identities
- Suppressing suspected nameplate draw signatures
- Investigating WoW's shared UI render path
- Investigating WoVR's UI render groups
- Testing separate left-eye UI rendering
- Testing independent UI render textures
- Testing per-eye UI compositing
- Investigating removal of the nameplate from only one eye
- Testing the original Blizzard nameplates
- Testing 3.3.5a Tidy Plates behavior

Several experiments successfully isolated portions of WoVR's rendering pipeline, but attempts to manipulate the nameplates independently also risked affecting unrelated systems such as UI rendering, mouse/controller collision, or an entire eye's rendered image.

Because the nameplates are intertwined with systems that are otherwise functioning correctly, increasingly aggressive modifications created a greater risk of introducing gameplay-breaking problems elsewhere.

### Why we're leaving it alone

After roughly **24 hours of trial, error, testing, rebuilding, and investigating the WoW/WoVR rendering pipeline**, we made the decision to leave the current behavior intact.

WoVR's core functionality is working:

- Head tracking works.
- Stereo 3D works.
- Motion/controller input works.
- UI interaction works.
- Combat and targeting work.
- Nameplates themselves still function.

The remaining issue is primarily visual.

At a certain point, fixing a cosmetic rendering quirk was no longer worth risking regressions to the systems that make the game playable in VR.

This project is about making World of Warcraft 3.3.5a enjoyable and practical to play in VR — not sacrificing a working build in pursuit of one stubborn nameplate. 🙂

### Could this be fixed someday?

Possibly.

A future solution would likely need to identify the nameplate earlier in WoW's rendering pipeline and give it proper VR-aware stereoscopic positioning, rather than attempting to modify the finished image afterward.

For now:

**Double nameplates are a known limitation of the WoVR Quest Community Build.**

And after ~24 hours of investigation...

**we promise, we noticed them too. 😂**

It breaks my heart that we weren't able to succeed in making the nameplates work. I'm hoping to revisit and tackle this problem later down the road. But for now, I'm going to continue playing with nameplates off and keep making my journey to take down the Lich King in VR! Along with fixing everything else I may encounter down the road. Till next time, Friends. I'll see you in Azeroth!

🎮 Controller Mapping Update — Stick Click Swap
Swapped the Left Stick Click and Right Stick Click action-slot bindings.
This makes the controller layout feel more natural and mentally consistent when moving through the action bar.
No functionality was added or removed — this is purely a control-layout improvement for easier muscle memory.

## Patch Notes — August 25, 2026

Updated bindings:

Left Stick Click: Action Slot 2
Grip + Left Stick Click: Action Slot 1
Right Stick Click: Action Slot 4
Grip + Right Stick Click: Action Slot 3

## Patch Notes — August 23, 2026

Healer-Friendly Targeting Update

LGrip + A now targets the nearest friendly player, making party and raid healing much more intuitive in VR.
RGrip + A remains Target Nearest Enemy, giving quick access to both friendly and hostile targets from the same button.
Map has been moved to LGrip + Right Trigger, replacing the previous backpack shortcut.
In-game setup: Bind Target Nearest Friendly Player to F8 in WoW's Key Bindings.

This update makes the controller layout significantly more healer-friendly while keeping combat targeting fast and accessible.

## Update — August 22, 2026

🎮 Controller Binding Update
Swapped the 5/6 and 9/10 action-slot mappings to create a more logical layout for kiting while moving in combat.
B: 10 | Grip + B: 9
X: 6 | Grip + X: 5
This places frequently used kiting abilities on more comfortable inputs while maintaining movement control.
No changes to the existing Y or thumbstick mappings.

🎮 Grip Modifier Camera Jerk Fix
Fixed unintended camera jerking/movement when using Grip-modified controls.
Corrected conflicts affecting:
Grip + Y
Grip + X
Grip + B
Grip + Left Stick Click
Grip + Right Stick Click
Normal button/stick actions are now properly suppressed while Grip is held, preventing the underlying camera controls from firing alongside the modified command.
Standard controls continue to function normally when Grip is not held.

- Fixed an issue where pressing **LGrip + A** to open the map while moving could cause the character to suddenly turn 180°.
- Removed unintended character-facing logic from the map input.
- **LGrip + A** now opens the map without affecting character movement or facing.

\---

# About This Project

The **WoVR Quest Community Patch** builds upon the original WoVR project created by **ProjectMimer and its original contributors**.

The original WoVR project provided the foundation that made World of Warcraft 3.3.5a VR possible.

Development of this community patch began after attempting to use the original WoVR source on a modern Meta Quest and SteamVR setup and encountering significant rendering, movement, camera, controller, and usability problems.

The original goal was simple:

**Get WoVR working properly again.**

That eventually became a much larger project involving:

* VR rendering fixes
* Stereoscopic image corrections
* Eye-flickering fixes
* Movement improvements
* Camera behavior changes
* Controller input fixes
* VR laser visibility improvements
* UI interaction troubleshooting
* Meta Quest controller optimization
* Independent Left and Right Grip detection
* Grip-button modifier support
* Complete Action Bar 1–12 controller access
* Two-page action-bar support
* Up to 24 controller-accessible ability slots
* Additional VR quality-of-life controls

The result is a substantially more comfortable and practical way to play World of Warcraft 3.3.5a in VR.

This is an **unofficial community modification** and is not an official ProjectMimer release.

\---

# Version 1.0 Changelog

## VR Rendering \& Visual Fixes

* Fixed severe rapid eye flickering that made the original build extremely uncomfortable or impractical to use.
* Corrected rendering behavior that could result in one eye displaying incorrectly or appearing black.
* Corrected stereoscopic rendering problems that caused the two eye views to appear improperly aligned or cross-eyed.
* Modified the rendering process to produce a substantially more stable VR image.
* Improved overall visual comfort during normal gameplay.
* Improved the visibility of the VR pointing and interaction system.
* Changed the VR laser/interaction endpoint to a more visible green appearance.
* Performed additional troubleshooting and modification of the VR rendering pipeline to improve compatibility with the tested SteamVR and Meta Quest configuration.

\---

# Locomotion \& Camera Improvements

* Reworked controller movement behavior for more natural VR locomotion.
* Fixed movement behavior that could cause the player's orientation or camera to abruptly rotate when changing movement direction.
* Eliminated extremely disorienting camera behavior that could effectively rotate the player's view approximately 180 degrees while changing direction.
* Improved directional movement so character control feels significantly smoother while using Quest thumbsticks.
* Corrected an issue where right-stick camera movement could unintentionally toggle the WoW character between walking and running.
* Improved horizontal right-stick camera control.
* Preserved head tracking independently from controller-based character movement.
* Improved overall seated-play usability.

\---

# VR UI Interaction Improvements

* Improved VR pointer interaction with the World of Warcraft interface.
* Verified VR interaction with inventory and bag windows.
* Verified VR interaction with the character window.
* Verified VR interaction with the quest interface.
* Corrected and verified interaction with the talent interface after troubleshooting VR UI input behavior.
* Preserved ability and UI tooltip functionality while using the VR pointer.
* Preserved normal left-click and right-click functionality through the Quest controller.

\---

# Meta Quest Controller Overhaul

The controller system has been substantially redesigned around **actual VR gameplay** rather than attempting to reproduce traditional keyboard controls.

Quest grip buttons function as modifiers, allowing the limited number of physical controller buttons to access an entire primary World of Warcraft action bar while preserving important movement, targeting, mouse, map, inventory, and jumping controls.

## VR Controller Layout

### 🎮 Action Bar

- **Left Stick Click** → Slot 2
- **Either Grip + Left Stick Click** → Slot 1
- **Right Stick Click** → Slot 4
- **Either Grip + Right Stick Click** → Slot 3
- **X** → Slot 6
- **Either Grip + X** → Slot 5
- **Y** → Slot 8
- **Either Grip + Y** → Slot 7
- **B** → Slot 10
- **Either Grip + B** → Slot 9
- **Left Trigger** → Slot 12
- **Right Grip + Left Trigger** → Slot 11
- **Left Grip + Left Trigger** → Switch Action Page

### 🕹️ Movement & Utility

- **Left Stick** → Character Movement
- **Right Stick** → Camera Control
- **A** → Jump
- **Right Grip + A** → Tab Target / Target Nearest Enemy
- **Left Grip + A** → F8
- **Right Trigger** → Left Mouse Click
- **Right Grip + Right Trigger** → Right Mouse Click
- **Left Grip + Right Trigger** → Open/Close Map

## Why is Left Grip + A = F8?

My reasoning for this is to have a comfortable keybinding that can be interchangeable in the ingame keybindings. So far example, when I first started playing with my build, i had it set to open back. Which is pretty useful if you have Bagnon. The Healer main in me also thought about changing it to Target Nearest Friendly Player so I can "tab target" my party members in dungeons, while reserving the second action bar page for focus macros for the tank. Personally, one thing I discovered while playing today is I dont have any way to natively swim or fly down with my control scheme. So right now my Left Grip + A is set to go down when flying or swimming. Luckily if feels natural considering swim/fly up and Jump are both mapped the Normal A button.

The action-bar assignments in the WoVR Quest Community Patch are intentionally designed around how the World of Warcraft interface appears while wearing a VR headset, rather than reproducing the traditional left-to-right keyboard layout.

The arrangement is also designed for comfortable kiting and combat while maintaining movement. Frequently used abilities can be activated with the face buttons and grip combinations without requiring the player to constantly remove their thumbs from the movement and camera controls.

## Right-to-Left Ability Progression

The controller layout intentionally progresses through abilities **from right to left instead of left to right**.

When playing World of Warcraft in VR, the left side of the action bar curves farther into the player's peripheral vision. Abilities positioned closer to the bottom-center portion of the interface are considerably easier to see without deliberately looking away from combat.

For this reason, the controller layout progresses:

**12 → 11 → 10 → 9 → 8 → 7 → 6 → 5 → 4 → 3 → 2 → 1**

rather than following a conventional left-to-right controller progression.

This allows players to place their **core rotation and most frequently monitored abilities toward the end of the action bar**, where they appear closer to the bottom-center of the VR display.

Keeping core abilities in this area makes it easier to:

* Monitor ability cooldowns.
* See when rotational abilities become available.
* Keep track of frequently used spells and attacks.
* Maintain visual attention on combat.
* Avoid repeatedly looking toward the curved peripheral portion of the VR interface.

Players remain completely free to organize their action bars however they prefer.

The right-to-left progression is simply designed to make the most visually important abilities easier to monitor while wearing the headset.

\---

# Why Is There Only One Action-Page Button?

Once WoW's additional action bars are enabled through the user interface, the primary hotkey bar only has **two available pages to cycle between**.

Because there are only two pages, separate **Previous Page** and **Next Page** controller buttons would effectively accomplish the same thing.

Either command simply alternates between:

**Action Page 1**

and

**Action Page 2**

Using two valuable Quest controller combinations for this would therefore be redundant.

The WoVR Quest Community Patch instead dedicates only:

**Left Grip + Left Trigger → Switch Action Page**

Pressing the combination switches to the other available primary action-bar page.

Pressing it again returns to the previous page.

This allowed another valuable controller combination to instead become:

**Left Grip + Right Trigger → Backpack**

This makes better use of the limited number of physical inputs available on the Quest controllers.

\---

# 24 Controller-Accessible Ability Slots

Each primary action-bar page contains:

**12 ability slots**

The Quest controller layout provides direct access to **all 12 slots** without requiring the player to reach for a keyboard.

With two usable primary action pages:

## **12 slots × 2 pages = 24 controller-accessible hotbar slots**

Those slots can be used for:

* Attacks
* Heals
* Spells
* Core rotation abilities
* Cooldowns
* Utility abilities
* Items
* Macros
* Other WoW hotbar actions

A player can therefore build a complete WoW control scheme while remaining inside VR and using the Quest motion controllers.

\---

# Controller Design Philosophy

The unusual numbering and grip-modifier system are deliberate.

The controller layout was designed around three primary goals:

1. **Keep core rotational abilities near the bottom-center of the VR display so cooldowns are easier to monitor.**
2. **Provide predictable right-to-left access to all 12 primary action-bar slots.**
3. **Use WoW's two available primary action pages to provide up to 24 controller-accessible ability slots without wasting another Quest input on redundant page switching.**

The result is not intended to imitate a keyboard.

It is intended to make World of Warcraft's existing interface and ability system feel natural when played **entirely from inside a VR headset using motion controllers**.

\---

# Input-System Improvements

Version 1.0 introduces significant changes to the underlying controller-input system.

* Added independent recognition of **Left Grip** and **Right Grip**.
* Preserved a combined **Either Grip** modifier for controls where the physical grip side does not matter.
* Added multi-function trigger behavior depending on which grip is held.
* Added state tracking for trigger combinations to prevent conflicting input behavior.
* Expanded available Quest controller commands without requiring additional physical buttons.
* Preserved standard mouse interaction while adding grip-modified trigger functions.
* Added dedicated backpack access.
* Added dedicated World Map access.
* Added controller-based nearest-enemy targeting.
* Preserved normal A-button jumping while adding two grip-modified A-button functions.
* Reorganized complete Action Bar 1–12 access around VR controller accessibility.

\---

# Installation Guide

The following procedure describes the configuration used during development and testing of the WoVR Quest Community Patch.

WoVR is designed around:

## **World of Warcraft 3.3.5a — Wrath of the Lich King**

Do not attempt to install this build into modern Retail World of Warcraft.

\---

# Step 1 — Obtain the Correct WoW 3.3.5a Client

During development and testing, a compatible World of Warcraft 3.3.5a client was obtained through **TheraWoW**.

When choosing the client, make sure you download/install the:

## **CLASSIC CLIENT**

### **Do NOT select the HD Texture Pack version.**

The WoVR Quest Community Patch was developed and tested using the standard **Classic World of Warcraft 3.3.5a client**, and compatibility with the HD-texture version has not been established.

For the most reliable experience, use:

**World of Warcraft 3.3.5a**

**Classic Client**

**No HD Texture Pack**

After downloading/installing the client, verify that the World of Warcraft directory contains the normal game files, including:

`Wow.exe`

Do not install the VR modification yet.

> \*\*Important:\*\* Starting with the correct client matters. If you accidentally install the HD Texture Pack version, obtain the standard Classic client before continuing rather than attempting to troubleshoot WoVR against an untested client configuration.

\---

# Step 2 — Create a ChromieCraft/Warmane account

## Update - August, 26, 2026

This Mod was just tested for Warmane and runs with no issues!!!



The WoVR Quest Community Patch was developed and tested while connecting to **ChromieCraft**.

Create the required ChromieCraft/game account using ChromieCraft's current registration instructions.

Complete the account setup before modifying the World of Warcraft client.

\---

# Step 3 — Change the Realmlist

A client obtained through TheraWoW may initially be configured to connect to the TheraWoW server.

To use the client with ChromieCraft, locate the World of Warcraft realmlist file.

This will normally be located inside a path similar to:

`Data\\enUS\\realmlist.wtf`

The locale folder may have a different name depending on the language of the client.

Open `realmlist.wtf` using Notepad or another plain-text editor.

Replace the existing server information with the **current ChromieCraft realmlist**.

Save the file.

> \*\*Important:\*\* Obtain the current realmlist directly from ChromieCraft rather than permanently relying on an address copied from this guide. Server configuration can change over time.

\---

# Step 4 — Clear the WoW Cache

After changing the realmlist:

1. Completely close World of Warcraft.
2. Locate the `Cache` folder inside the WoW installation.
3. Delete the `Cache` folder.

Do **not** delete the `Data` folder.

World of Warcraft will automatically recreate its Cache folder when the game launches again.

Clearing the cache helps prevent old server information from interfering with the new realmlist configuration.

\---

# Step 5 — Test Desktop WoW First

Before installing WoVR:

1. Launch `Wow.exe` normally.
2. Confirm that World of Warcraft reaches the login screen.
3. Log into the ChromieCraft account.
4. Confirm that the client successfully connects.
5. Reach the character-selection screen.
6. Enter the game normally at least once.

Do not continue to VR troubleshooting until ordinary desktop World of Warcraft works correctly.

This makes it significantly easier to distinguish a **WoW/server problem** from a **WoVR/SteamVR problem**.

\---

# Step 6 — Prepare SteamVR and Meta Quest

Install Steam and **SteamVR** if they are not already installed.

Connect the Meta Quest headset to the PC using the user's preferred supported PC-VR connection method.

Launch SteamVR.

Before continuing, verify:

* The headset is detected.
* Both Quest controllers are detected.
* Head tracking works.
* SteamVR itself operates normally.

If SteamVR cannot correctly detect the headset or controllers, correct that issue before troubleshooting WoVR.

\---

# Step 7 — Install the Required WoVR Files

The working WoVR setup requires **three components**:

`d3d9.dll`

`openvr\_api.dll`

`vr` folder

Copy all three directly into the main World of Warcraft directory containing `Wow.exe`.

The finished directory should resemble:

```text id="m7g19q"
World of Warcraft\\
├── Wow.exe
├── d3d9.dll
├── openvr\_api.dll
├── vr\\
└── \[normal WoW files and folders]
```

Do **not** place these components inside:

`Data`

`Interface`

or

`WTF`

The entire `vr` folder must remain intact.

Do not remove individual files from the `vr` folder or scatter its contents throughout the WoW installation.

The `vr` folder contains files required by WoVR, including VR configuration information, OpenVR action files, and interface assets.

\---

# Step 8 — Back Up a Working DLL

Once WoVR is working correctly, create a **copy** of:

`d3d9.dll`

Rename the copy:

`d3d9\_old.dll`

Leave the active version named:

`d3d9.dll`

The directory can then contain:

```text id="x28gdu"
d3d9.dll       ← Active WoVR build
d3d9\_old.dll   ← Known-good backup
```

This provides a quick recovery option if a future patch or modification causes problems.

\---

# Step 9 — First VR Launch

With the Meta Quest connected:

1. Start SteamVR.
2. Verify that the headset and controllers appear normally.
3. Launch WoW using the configured WoVR installation.
4. Allow WoW to initialize through SteamVR.
5. Log into the game.
6. Enter the world.

Verify that:

* Both eyes display correctly.
* The image remains stable.
* Head tracking works.
* Character movement works.
* Quest controller inputs respond.
* The VR pointer/laser appears.
* World of Warcraft interface elements can be interacted with.

\---

# Step 10 — Required WoW Keybinding Change

The community controller configuration requires an important change to WoW's default action-page bindings.

Inside World of Warcraft, open:

**Esc → Key Bindings**

Locate the Action Bar functions responsible for changing action pages.

The default configuration uses:

**Previous Action Bar → Shift + Up Arrow**

**Next Action Bar → Shift + Down Arrow**

Change these to:

**Previous Action Bar → Up Arrow**

**Next Action Bar → Down Arrow**

The WoVR keyboard-input implementation did not reliably transmit the original modifier-plus-arrow combination during development.

Using plain arrow keys allows the VR controller to reliably send the required action-page command.

Because only two primary action pages need to be cycled between once the additional action bars are enabled, the controller only requires one page-switch command.

This keybinding change is **required for the VR action-page control to function correctly**.

\---

# Step 11 — Configure Your Action Bars

Once the controller is working, arrange your abilities according to personal preference.

The controller layout progresses **from right to left** so that the end of the action bar can be used for your **core rotation and most frequently used abilities**.

This portion of the action bar appears closer to the bottom-center of the VR interface, making important abilities and cooldowns easier to monitor during combat.

The remaining slots can be used for secondary rotational abilities, utility spells, cooldowns, macros, items, and situational abilities.

Once WoW's additional action bars are enabled, the two primary pages provide:

## **Up to 24 controller-accessible hotbar slots**

How those slots are organized is entirely up to the player.

\---

# Troubleshooting

## Realmlist Keeps Changing Back

Completely close World of Warcraft before modifying `realmlist.wtf`.

Save the correct ChromieCraft realmlist and clear the WoW Cache folder.

If the client continues restoring another server's configuration, verify that:

* The correct `realmlist.wtf` is being edited.
* WoW was completely closed while editing.
* A server-specific launcher is not rewriting the configuration.

Once the correct realmlist has been configured, launch through `Wow.exe` rather than unnecessarily running another server's launcher.

\---

## WoW Works Normally but VR Does Not

First verify that SteamVR works independently.

Confirm that all three required WoVR components are inside the directory containing `Wow.exe`:

`d3d9.dll`

`openvr\_api.dll`

`vr` folder

Make sure the entire `vr` folder remains intact.

\---

## VR Pointer Works in Some Windows but Not Others

VR UI interaction has been tested with major World of Warcraft interface elements including:

* Bags
* Character interface
* Quest interface
* Talent interface

If a particular interface temporarily refuses VR interaction, verify that the same interface functions normally outside VR and reopen it before further troubleshooting.

\---

# d3d9.dll / Bad Image Error

If Windows displays a **Bad Image** error involving `d3d9.dll`, you do **not** need Visual Studio and you should not attempt to compile or modify the source code.

The normal release of the WoVR Quest Community Patch provides a prebuilt and tested `d3d9.dll`.

First:

1. Completely close World of Warcraft and SteamVR.
2. Open the main World of Warcraft directory containing `Wow.exe`.
3. Delete the current `d3d9.dll`.
4. Obtain a fresh copy of `d3d9.dll` from the WoVR Quest Community Patch package.
5. Copy the fresh DLL directly beside `Wow.exe`.
6. Verify that `openvr\_api.dll` and the complete `vr` folder are also present.
7. Restart SteamVR.
8. Launch World of Warcraft again.

### If the Error Continues

Do **not** download random `d3d9.dll` files from DLL-download websites.

Instead, obtain a fresh copy of the WoVR Quest Community Patch package.

Windows may occasionally block files downloaded from the internet.

Right-click the downloaded ZIP or affected file and select:

**Properties**

Look near the bottom of the **General** tab for an:

**Unblock**

option.

If it appears:

1. Check **Unblock**.
2. Select **Apply**.
3. Select **OK**.
4. Extract the WoVR files again.

If no Unblock option appears, continue normally.

If the error still occurs after installing fresh copies of the patch files, report the issue and include:

* Windows version
* Headset model
* Exact error message or screenshot
* Confirmation that the **Classic 3.3.5a client without the HD Texture Pack** is being used
* Confirmation that `d3d9.dll`, `openvr\_api.dll`, and the complete `vr` folder are beside `Wow.exe`

Normal players should **not need Visual Studio, source code, or compilation tools** to install or troubleshoot the WoVR Quest Community Patch.

\---

# Version 1.0 Testing Status

The current stable Version 1.0 configuration has been tested for:

* VR startup
* SteamVR integration
* Meta Quest operation
* Stereoscopic rendering
* Eye-image stability
* Head tracking
* Character locomotion
* Camera movement
* Quest controller input
* Independent Left/Right Grip detection
* Either-Grip modifiers
* Action Bar Slots 1–12
* Two-page action-bar switching
* Up to 24 controller-accessible hotbar slots
* Left mouse click
* Right mouse click
* Jumping
* Backpack access
* World Map access
* Tab targeting / Target Nearest Enemy
* VR pointer/laser functionality
* Major WoW UI interaction
* Seated gameplay

The modified WoVR setup has also successfully operated on an additional PC/setup beyond the primary development system.

\---

# Credits

## Original WoVR

**ProjectMimer and the original WoVR contributors**

The WoVR Quest Community Patch would not exist without the original developers who created the underlying WoVR implementation.

Their work provided the foundation that made this community effort possible.

All credit for the original WoVR implementation belongs to its respective creators and contributors.

\---

## WoVR Quest Community Patch

This community patch focuses on restoring, improving, and expanding WoVR functionality for modern VR use, with particular emphasis on:

* Meta Quest controller support
* VR comfort
* Rendering stability
* Locomotion
* Camera behavior
* Controller accessibility
* UI usability
* Complete VR-based ability access

The project is an **unofficial community modification**.

It is not an official ProjectMimer release and should not be interpreted as being affiliated with or endorsed by ProjectMimer.

\---

# Trademark Notice

World of Warcraft and related properties belong to Blizzard Entertainment.

SteamVR belongs to Valve Corporation.

Meta Quest belongs to Meta Platforms.

All other trademarks, product names, and intellectual property belong to their respective owners.

\---

# Project Status

**Version:** 1.0 Stable

**Game:** World of Warcraft 3.3.5a — Wrath of the Lich King

**Required Client:** Classic 3.3.5a — No HD Texture Pack

**VR Runtime:** SteamVR

**Primary Tested Headset:** Meta Quest

**Controller:** Meta Quest motion controllers

**Available Primary Ability Inputs:** 12 per action page

**Usable Primary Action Pages:** 2

**Total Controller-Accessible Hotbar Slots:** Up to 24

**Development Status:** Stable community build / continued testing

Future development may include additional compatibility improvements, controller refinements, documentation improvements, bug fixes, and community-reported improvements.

