# Roblox Teleporter Script

A secure and feature-rich **Server Script** for Roblox that allows players to teleport between two parts (`teleporter1` and `teleporter2`) with smooth visual effects.

## Features
- **Two-Way Teleportation:** Seamlessly teleports players back and forth between two designated parts.
- **Visual Effects:** Triggers a blue glowing highlight and particle spark effects using Roblox's `Debris` service.
- **Cooldown System:** Prevents spamming and infinite teleport loops per player.
- **Safety Checks:** Verifies player health, character existence, and handles cleanups when players leave the game.

## Installation & Usage

1. Open your place in **Roblox Studio**.
2. Create two Parts in your Workspace and name them exactly `teleporter1` and `teleporter2`.
3. Insert a standard **Script** (not a LocalScript) into **ServerScriptService** (or Workspace).
4. Paste the code from `TeleporterScript.lua` into the script.
5. Playtest your game and step on the teleporters!
