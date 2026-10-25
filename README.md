# Hello World Minecraft Server — Client Setup

This repository is the shared download location for the client files used to join our modded Minecraft Java world. The server's mod list and shaderpack can change over time, so check here for updates before joining.

## Getting started

- [`README.md`](README.md) — setup instructions, compatibility notes, and guidance for suggesting changes.
- [`mods/`](mods/) — NeoForge mod `.jar` files. Some add gameplay or world-generation content; others provide client-side features or are required libraries for another mod.
- [`shaderpacks/`](shaderpacks/) — shaderpack files. Shaders are optional and can have a large effect on performance.
- [`neoforge-21.1.251-installer.jar`](neoforge-21.1.251-installer.jar) — the NeoForge installer for the server's Minecraft 1.21.1 setup.

Use the versions in this repository as a set. The server owner may update, add, or remove files; check the repository again when the server's mods change.

## Set up your client

1. **Install Java 21.** Minecraft 1.21.1 uses Java 21. Install a Java 21 runtime from a trusted Java provider, then restart the Minecraft Launcher if it was open.
2. **Install Minecraft: Java Edition.** Install the official Minecraft Launcher, sign in with an account that owns Java Edition, and launch Minecraft 1.21.1 once. Close the game and launcher before continuing.
3. **Install NeoForge.** Download this repository's `neoforge-21.1.251-installer.jar` (or the current installer if the owner has updated it). Open the installer and choose **Install client**. If Windows asks which app should open the `.jar`, select Java 21. The installer should create a NeoForge profile in the Minecraft Launcher.
4. **Create or select the NeoForge installation.** In the Launcher, open **Installations** and select the NeoForge 1.21.1 installation that the installer created. If it is not listed, enable the **Modded** filter or restart the Launcher. Use the installation's **Edit** option to view its settings. Leave **Game Directory** set to the default unless you have a reason to change it; if you choose a custom directory, use that directory for the pack folders in the next step.
5. **Open the installation's game folder.** In **Installations**, find the NeoForge row and click its folder icon (hovering shows **Open installations folder**). This opens the installation folder. To find the active game directory, open **Edit** and check **Game Directory**. If it says **Use default directory**, the game uses `.minecraft`; on Windows you can open it with `Win+R` → `%AppData%\.minecraft`. If the Edit page offers **click here** to use the `.minecraft` game directory, select it to use that location. Copy the pack into the active game directory, not the folder containing the installer.
6. **Copy the pack folders.** Download this repository using **Code → Download ZIP** on GitHub and extract it. Copy the `mods` and `shaderpacks` folders from the extracted repository into the active game directory from step 5. If Windows asks to merge folders, choose to merge; if asked about a same-named file, use the newer repository copy. The result should be `<game directory>\mods` and `<game directory>\shaderpacks`, with the `.jar` files directly inside `mods` (not in an extra nested `mods` folder).
7. **Start the game.** In the Launcher, select the NeoForge installation and click **Play**. If it fails to load, check that you used Java 21 and Minecraft 1.21.1, and that you copied the current mod files.
8. **Optional: turn on the shader.** The pack includes Iris and the Complementary Reimagined shaderpack. In game, open **Options → Video Settings → Shader Packs** and select Complementary Reimagined. Leave shaders disabled if performance is poor.

Do not put the installer `.jar` in the `mods` folder. Do not replace or delete your `.minecraft\saves` folder. When updating, merge the current `mods` and `shaderpacks` folders into the active game directory; remove outdated mod versions when replacing them so that only one version of each mod remains.

### Memory and JVM arguments

The Launcher installation's **Edit → JVM Arguments** field controls Java memory and startup options. Most players should keep the launcher's default arguments; no special JVM tuning is required. Do not paste the gaming-PC settings below on top of existing arguments—replace the field contents if you decide to use them, and keep only one `-Xmx` option.

For a capable gaming PC with **at least 16 GB of system RAM** (and no other memory-intensive programs running), the server owner's current example is:

```text
-Xmx8G -XX:+UseZGC -XX:+UnlockExperimentalVMOptions -XX:+ZGenerational -XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+PerfDisableSharedMem
```

This gives Minecraft up to 8 GB of heap, and `AlwaysPreTouch` can commit that memory up front, increasing startup time and memory pressure. It is not a universal performance boost. On a PC with less RAM, or if you notice slowdowns outside Minecraft, leave the default JVM arguments in place. If Minecraft reports out-of-memory errors, close other programs first; only then consider setting a smaller heap such as `-Xmx4G` or `-Xmx6G`, while leaving the other arguments at their defaults. Always leave enough memory for Windows and other running programs.

## Server information

**Current hosting:** The server currently runs on the owner's PC while the owner is online and playing Minecraft. It may not be available when the owner is offline. Ask the owner for the server address and to confirm that the server is running before connecting.

**Dedicated server — coming soon:** The plan is to move the world to a separate retired desktop PC so it can run 24/7. Hosting details and connection instructions will be added here once that server is set up.

## Optional mods and performance

For the most reliable connection, start with **all** mods in the repository. Some mods add blocks, items, recipes, structures, or world-generation features that the server expects. Removing one may prevent you from joining, cause missing content, or make your client incompatible. Library/dependency mods are also needed even if they do not have an obvious in-game feature.

The following current mods are client-side features and are generally the first ones to try removing if your computer struggles. Remove only the named `.jar`; leave the rest of the pack intact. If a mod warns that another mod depends on it, keep it. If you are unsure whether a change is safe, ask the server owner.

| Mod file(s) in `mods/` | What it does / performance note |
| --- | --- |
| `DistantHorizons-3.3.3-1.21.1.jar` | Renders distant terrain beyond the normal view distance. Can use substantial memory, CPU, and disk space while generating its detail; a good first mod to omit on a low-end PC. |
| `lambdynamiclights-4.8.11+1.21.1.jar` | Dynamic lights carried by players and items; can affect rendering performance. |
| `iris-neoforge-1.8.12+mc1.21.1.jar`, `sodium-neoforge-0.6.13+mc1.21.1.jar` | Shader and rendering enhancements. Keep both when using the included shaderpack; without them, play without shaders using the normal renderer. |
| `ComplementaryReimagined_r5.9.3.zip` in `shaderpacks/` | Optional shader effects. Disabling/removing this shaderpack is the best first step if frame rate is low. Shader quality settings also have a large impact. |
| `sound-physics-remastered-neoforge-1.21.1-1.5.1.jar`, `sounds-2.4.22+lts+1.21.1-neoforge.jar`, `Drip Sounds-0.5.2+1.21.8-NeoForge.jar` | Optional audio effects. Usually less demanding than shaders, but can be removed if needed. |
| `fallingleaves-1.21.1-2.5.1.jar`, `visuality-forge-3.0.0.jar` | Optional visual particles and effects; try removing these to reduce visual clutter or rendering work. |
| `entityculling-neoforge-1.11.2-mc1.21.1.jar`, `ImmediatelyFast-NeoForge-1.6.14+1.21.1.jar` | Client rendering/performance features. Normally leave these installed; if troubleshooting a graphics issue, test without them one at a time. |
| `freecam-neoforge-1.3.0+mc1.21.jar`, `xaerominimap-neoforge-1.21.1-26.5.0.jar`, `xaeroworldmap-neoforge-1.21.1-1.46.0.jar` | Optional camera and map features. Remove if you do not use them. |
| `appleskin-neoforge-mc1.21-3.0.9.jar`, `jei-1.21.1-neoforge-19.57.0.446.jar`, `LegendaryTooltips-1.21.1-neoforge-1.5.5.jar`, `MouseTweaks-neoforge-mc1.21-2.26.1.jar`, `statuseffectbars-1.21.1-NeoForge-1.0.2.jar` | Optional interface and quality-of-life features; remove any you do not want. |

**Version check:** `Drip Sounds-0.5.2+1.21.8-NeoForge.jar` has `1.21.8` in its filename, while this pack targets Minecraft 1.21.1. Confirm its supported version with the server owner before relying on it; if it causes a startup error, remove it and let the owner know.

Most other mods, especially world-generation/content mods and libraries, should be treated as **required unless the server owner says otherwise**. Removing mods is not a substitute for lowering Minecraft's render distance, simulation distance, or shader quality. For a low-end PC, first disable the shader, then try omitting Distant Horizons and optional visual/audio effects.

## Updating your files

The `mods/` and `shaderpacks/` folders are maintained by the server owner and can change as the world changes. Before joining after an update, download the latest repository ZIP and merge its `mods` and `shaderpacks` folders into `.minecraft`. Remove old versions of updated `.jar` files to avoid duplicate-version conflicts. Keep your worlds and other `.minecraft` data.

GitHub's commit history records each addition, removal, and update, so a separate changelog is not required. Check **Commits** on the repository page to see what changed. When making pack updates, descriptive commit messages (for example, `Add mod-name 1.2.3` or `Update mod-name to 1.2.3`) make it easier to identify a change if it causes a problem.

## Finding and suggesting mods

You can browse mods on [Modrinth](https://modrinth.com/mods) (recommended) or [CurseForge](https://www.curseforge.com/minecraft/search?class=mc-mods).

1. Search for the mod and open its project page.
2. Filter/select **Minecraft 1.21.1** as the game version and **NeoForge** as the mod loader. Check the specific file's supported game version and loader before downloading; a Forge, Fabric, or different Minecraft version file will not work in this pack.
3. Download the mod file. Install dependencies listed by the mod author if they are not already in this repository. For a shader, download the shaderpack file instead of a mod `.jar`.
4. To test a mod locally, put its `.jar` in `.minecraft\mods`; put shaderpack files in `.minecraft\shaderpacks`. A local mod installation does **not** add the mod to the server. Do not join the world with an unapproved mod that changes gameplay or world content.
5. To suggest adding or updating something to the shared pack, open this repository on GitHub. If you have write access, use **Add file → Upload files**, select the new file(s), and commit with a descriptive message. Otherwise, fork the repository, upload the file(s) into the appropriate `mods` or `shaderpacks` folder in your fork, commit the change, and open a **Pull request** to this repository. Include the project link, exact version, Minecraft version, NeoForge compatibility, dependencies, and why you suggest it.
6. Wait for the server owner to review and test the change before treating it as part of the pack. New gameplay/world-generation mods may need to be installed on the server too, and some changes may not be safe to add to an existing world.

Do not remove or replace existing files in the shared pack without coordinating with the server owner. The commit history and pull requests help everyone see who changed the pack and what was added or removed.
