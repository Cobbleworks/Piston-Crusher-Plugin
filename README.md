<p align="center">
  <img src="images/plugin-logo.png" alt="Piston Crusher Plugin" width="180" />
</p>
<h1 align="center">Piston Crusher Plugin</h1>
<p align="center">
  <b>Automate block crushing using piston mechanics.</b><br>
  <b>Configurable whitelist, multiplier, crusher block type, and live admin commands.</b>
</p>
<p align="center">
  <a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/releases"><img src="https://img.shields.io/github/v/release/Cobbleworks/Piston-Crusher-Plugin?include_prereleases&style=flat-square&color=4CAF50" alt="Latest Release"></a>&nbsp;&nbsp;<a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License"></a>&nbsp;&nbsp;<img src="https://img.shields.io/badge/Java-17+-orange?style=flat-square" alt="Java Version">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Minecraft-1.20+-green?style=flat-square" alt="Minecraft Version">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Platform-Spigot%2FPaper-yellow?style=flat-square" alt="Platform">&nbsp;&nbsp;<img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square" alt="Status">&nbsp;&nbsp;<a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/issues"><img src="https://img.shields.io/github/issues/Cobbleworks/Piston-Crusher-Plugin?style=flat-square&color=orange" alt="Open Issues"></a>
</p>

Piston Crusher is an open-source Minecraft automation plugin that turns piston interactions into configurable block-crushing mechanics. When a piston extends and a whitelisted block is pushed into the configured crusher block, the target block is removed and item drops are generated using the configured multiplier. The plugin stores persistent runtime settings in data files (`whitelist.yml`, `crusherblock.yml`) and exposes all management operations through `/pistoncrusher` commands.

### **Core Features**

- **Whitelist-Driven Crushing:** Only materials on the plugin whitelist are eligible for crushing
- **Multiplier Control:** Set a global drop multiplier (minimum `1.0`) via command
- **Custom Crusher Block:** Choose the block that acts as the crusher target in the piston line
- **Runtime Administration:** Manage whitelist, multiplier, and crusher block without restart
- **Persistent Settings:** Whitelist and crusher block are saved in plugin data files
- **Tab Completion:** Subcommands and material names are suggested automatically

### **Supported Platforms**

- **Server Software:** `Spigot`, `Paper`, `Purpur`, `CraftBukkit`
- **Minecraft Versions:** `1.20` and higher
- **Java Requirements:** `Java 17+`

### **Installation**

1. Download the latest `.jar` from the [Releases](https://github.com/Cobbleworks/Piston-Crusher-Plugin/releases) page
2. Stop your Minecraft server
3. Copy the `.jar` into your server`s `plugins/` folder
4. Start your server -- the plugin creates `plugins/PistonCrusher/whitelist.yml` and `plugins/PistonCrusher/crusherblock.yml`

### **Setup Example**

To build a working piston crusher, arrange blocks in a straight line:

```
[Piston] --> [Block to Crush] --> [Crusher Block]
```

- The piston must face directly toward the candidate block
- The candidate block must be on the whitelist
- The block in front of that candidate must match the configured crusher block material
- On success, the candidate block is removed and dropped according to the multiplier

### **Administrative Commands**

| Command | Description |
|---------|-------------|
| `/pistoncrusher` | Show command usage |
| `/pistoncrusher whitelist add <material>` | Add a material to the crush whitelist |
| `/pistoncrusher whitelist remove <material>` | Remove a material from the crush whitelist |
| `/pistoncrusher whitelist list` | Display all currently whitelisted materials |
| `/pistoncrusher multiplier <value>` | Set the drop multiplier (values below `1` are clamped to `1`) |
| `/pistoncrusher multiplier` | Display the current output multiplier |
| `/pistoncrusher crusherblock <material>` | Set the designated crusher block type |
| `/pistoncrusher crusherblock` | Display the current crusher block material |

### **Data Files**

The plugin does not use a standard `config.yml`; instead, it persists state in dedicated files:

| File | Key | Default | Description |
|------|-----|---------|-------------|
| `plugins/PistonCrusher/whitelist.yml` | `whitelist` | `[COBBLESTONE]` | Materials eligible for crushing |
| `plugins/PistonCrusher/crusherblock.yml` | `crusherblock` | `WAXED_CHISELED_COPPER` | Block material that acts as crusher target |

### **Permissions**

| Permission | Description | Default |
|------------|-------------|---------|
| `pistoncrusher.admin` | Access to all `/pistoncrusher` commands | `op` |

### **Notes**

- Material values must be valid Bukkit material names (for example `cobblestone`, `stone`, `gold_block`)
- Only movable blocks are accepted in whitelist/crusher-block operations
- Multiplier updates are runtime-only and reset on restart in current implementation

### **License**

This project is licensed under the **MIT License** -- see the [LICENSE](LICENSE) file for details.


## **Screenshots**

The screenshots below demonstrate Piston Crusher Plugin in action, including emerald block crushing, multiple crusher alignment, automated cobblestone farms, and the full range of built-in features.

<table>
  <tr>
    <th>Piston Crusher - Emerald Crushing</th>
    <th>Piston Crusher - Multiple Crushers</th>
  </tr>
  <tr>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-emerald-crushing.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-emerald-crushing.png" alt="Crusher machine crushing emerald blocks" width="450"></a></td>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-multiple-crushers.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-multiple-crushers.png" alt="Multiple piston crushers aligned nearby" width="450"></a></td>
  </tr>
  <tr>
    <th>Piston Crusher - Cobblestone Farm</th>
    <th>Piston Crusher - Gold Crush</th>
  </tr>
  <tr>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-cobblestone-farm.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-cobblestone-farm.png" alt="Automatic cobblestone farm with crusher" width="450"></a></td>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-gold-crush.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-gold-crush.png" alt="Gold block crushing" width="450"></a></td>
  </tr>
  <tr>
    <th>Piston Crusher - Auto Generator</th>
    <th>Piston Crusher - Block Arrangement</th>
  </tr>
  <tr>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-auto-generator.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-auto-generator.png" alt="Automatic generator setup" width="450"></a></td>
    <td><a href="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-block-arrangement.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/Cobbleworks/Piston-Crusher-Plugin/raw/main/images/screenshot-block-arrangement.png" alt="Block arrangement example" width="450"></a></td>
  </tr>
</table>
