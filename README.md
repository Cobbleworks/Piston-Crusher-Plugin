<p align="center">
  <img src="https://github.com/BerndHagen/Minecraft-Server-Plugins/raw/main/img/img_v1.0.1-mcplugin.png" alt="Piston Crusher" width="128" />
</p>
<h1 align="center">Piston Crusher</h1>
<p align="center">
  <b>Automate block crushing using piston mechanics.</b><br>
  <b>Configurable whitelist, output multipliers, and live-reload commands.</b>
</p>
<p align="center">
  <a href="https://github.com/Cobbleworks/Piston-Crusher/releases"><img src="https://img.shields.io/github/v/release/Cobbleworks/Piston-Crusher?include_prereleases&style=flat-square&color=4CAF50" alt="Latest Release"></a>&nbsp;&nbsp;<a href="https://github.com/Cobbleworks/Piston-Crusher/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License"></a>&nbsp;&nbsp;<img src="https://img.shields.io/badge/Java-17+-orange?style=flat-square" alt="Java Version">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Minecraft-1.21+-green?style=flat-square" alt="Minecraft Version">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Platform-Spigot%2FPaper-yellow?style=flat-square" alt="Platform">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square" alt="Status">
</p>

Piston Crusher is an open-source Minecraft automation plugin that turns pistons into configurable block-crushing machines. When a piston extends and pushes a whitelisted block into a designated crusher block, the block is destroyed and drops a multiplied number of items directly into the world. All settings — including the whitelist, output multiplier, and crusher block type — can be changed at runtime via commands without any server restart. Only physically moveable blocks qualify as crusher blocks, preventing abuse with immovable materials such as bedrock or obsidian.

### **Core Features**

- **Block Whitelist System:** Only blocks that are explicitly added to the whitelist can be crushed — all other blocks pass through the piston normally
- **Configurable Output Multiplier:** Controls how many items are dropped per crushed block — fractional values are supported (e.g., `2.5` drops 2 or 3 items with weighted randomness)
- **Crusher Block Selection:** Any piston-moveable block can be designated as the crusher target — the block must be directly adjacent to the block being pushed by the piston
- **Live Configuration:** All whitelist, multiplier, and crusher block changes take effect immediately without restarting the server
- **Full Tab Completion:** All material names in whitelist commands are tab-completed for accurate and fast configuration

### **Supported Platforms**

- **Server Software:** `Spigot`, `Paper`, `Purpur`, `CraftBukkit`
- **Minecraft Versions:** `1.21.5`, `1.21.6`, `1.21.7`, `1.21.8`, `1.21.9`, `1.21.10` and higher
- **Java Requirements:** `Java 17+`

### **Installation**

1. Download the latest `.jar` from the [Releases](https://github.com/Cobbleworks/Piston-Crusher/releases) page
2. Stop your Minecraft server
3. Copy the `.jar` into your server's `plugins` folder
4. Start your server — a default configuration folder is generated at `plugins/PistonCrusher/`

### **Setup Example**

To build a working piston crusher, arrange blocks in a straight line:

```
[Piston] → [Block to Crush] → [Crusher Block]
```

- When the piston extends, it pushes the block to crush into the crusher block
- If the pushed block is on the whitelist, it is destroyed and drops the configured multiplied item count
- The piston must face directly toward the block being crushed
- The crusher block must be piston-moveable (obsidian, bedrock, etc. are not valid)

### **Administrative Commands**

| Command | Description |
|---------|-------------|
| `/pistoncrusher whitelist add <Material>` | Add a block material to the crush whitelist |
| `/pistoncrusher whitelist remove <Material>` | Remove a block material from the whitelist |
| `/pistoncrusher whitelist list` | Display all currently whitelisted materials |
| `/pistoncrusher multiplier <Value>` | Set the item drop multiplier (e.g., `2.5`) |
| `/pistoncrusher multiplier` | Display the current output multiplier |
| `/pistoncrusher crusherblock <Material>` | Set the designated crusher block type |
| `/pistoncrusher crusherblock` | Display the current crusher block material |

**Note:** Material names must be valid Bukkit material names (e.g., `cobblestone`, `gold_block`). The multiplier must be `1.0` or greater. All changes take effect immediately.

### **License**

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
