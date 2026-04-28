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
- **Dependencies:** None - fully self-contained, no external plugins required

## **Table of Contents**

1. [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation Steps](#installation-steps)
    - [First Launch](#first-launch)
    - [Verifying Installation](#verifying-installation)
2. [Configuration](#configuration)
    - [Data Files](#data-files)
3. [How It Works](#how-it-works)
4. [Setup Example](#setup-example)
5. [Administrative Commands](#administrative-commands)
6. [Permissions](#permissions)
7. [Building from Source](#building-from-source)
8. [License](#license)
9. [Screenshots](#screenshots)

## **Getting Started**

### **Prerequisites**

Before installing Piston Crusher, confirm the following requirements are met:

- A Minecraft server running **Spigot**, **Paper**, **Purpur**, or any compatible fork
- Server version **1.20 or higher** (`api-version: 1.20` is the minimum)
- **Java 17** or newer installed on the machine running the server
- Operator or console access to install plugin files

No additional plugins or libraries are needed. Piston Crusher has zero external dependencies.

### **Installation Steps**

1. Download the latest `.jar` from the [Releases](https://github.com/Cobbleworks/Piston-Crusher-Plugin/releases) page
2. **Stop your server completely** before placing any files
3. Copy the `.jar` into your server's `plugins/` directory
4. Start the server - Piston Crusher generates its configuration folder automatically on first boot

### **First Launch**

On the first server start after installation, Piston Crusher creates the following structure:

```
plugins/
└── PistonCrusher/
    ├── whitelist.yml      - Materials eligible for crushing (default: COBBLESTONE)
    └── crusherblock.yml   - The block material used as crusher target (default: WAXED_CHISELED_COPPER)
```

The plugin is ready to use immediately after installation. To build a working crusher, arrange blocks according to the [Setup Example](#setup-example) section.

### **Verifying Installation**

- Run `/plugins` in-game - `PistonCrusher` should appear green in the list
- Run `/pistoncrusher whitelist list` to confirm the default whitelist is loaded
- Place a cobblestone block between a piston and a waxed chiseled copper block and fire the piston - the cobblestone should be crushed and drop items
- If the plugin fails to load, check the server console for `PistonCrusher` error messages (common causes: wrong Java version, corrupt JAR, or unsupported API version)

## **Configuration**

### **Data Files**

Piston Crusher does not use a standard `config.yml`; instead it persists state in dedicated files:

| File | Key | Default | Description |
|------|-----|---------|-------------|
| `plugins/PistonCrusher/whitelist.yml` | `whitelist` | `[COBBLESTONE]` | Materials eligible for crushing |
| `plugins/PistonCrusher/crusherblock.yml` | `crusherblock` | `WAXED_CHISELED_COPPER` | Block material that acts as crusher target |

> **Note:** Material values must be valid Bukkit material names (for example `cobblestone`, `stone`, `gold_block`). Only movable blocks are accepted.

## **How It Works**

When a piston is fired, Piston Crusher intercepts the `BlockPistonExtendEvent`. It checks every block that the piston is about to push in order. If the piston encounters a block that is on the whitelist **and** the block directly ahead of it matches the configured crusher block material, the following happens:

1. The candidate block (the whitelisted one) is removed from the world
2. Item drops are spawned at that location
3. The drop quantity is multiplied by the configured multiplier (minimum `1.0`)

The piston itself does not physically move the block - the event is cancelled for the target block so Minecraft's built-in pushing behavior does not apply. All other blocks in the push line that are not whitelisted are pushed normally.

## **Setup Example**

To build a working piston crusher, arrange blocks in a straight line:

```
[Piston] --> [Block to Crush] --> [Crusher Block]
```

- The piston must face directly toward the candidate block
- The candidate block must be on the whitelist
- The block directly in front of the candidate must match the configured crusher block material
- On success, the candidate block is removed and its drops are spawned with the configured multiplier applied

## **Administrative Commands**

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

## **Permissions**

| Permission | Description | Default |
|------------|-------------|---------|
| `pistoncrusher.admin` | Access to all `/pistoncrusher` commands | `op` |

## **Building from Source**

Piston Crusher uses **Apache Maven** as its build system. The plugin is packaged as a standard JAR with no external runtime dependencies.

**Requirements:**
- Java 17 or newer
- Apache Maven 3.6 or newer

**Steps:**

```bash
# Clone the repository
git clone https://github.com/Cobbleworks/Piston-Crusher-Plugin.git
cd Piston-Crusher-Plugin

# Compile and package
mvn clean package
```

The output JAR is written to `target/Piston-Crusher-x.x.x.jar`. Copy it into your server's `plugins/` folder as described in the [Installation Steps](#installation-steps) section.

**Project Structure:**

```
src/main/
├── java/org/example/
│   ├── PistonCrusherPlugin.java   - Plugin entry point (onEnable / onDisable)
│   ├── PistonCrusherListener.java - Piston extend event handling and crush logic
│   └── PistonCrusherCommand.java  - All /pistoncrusher subcommands + tab completion
└── resources/
    └── plugin.yml                 - Plugin metadata, commands, permissions
```

## **License**

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## **Screenshots**

The screenshots below demonstrate Piston Crusher in action, including emerald block crushing, multiple crusher alignment, and automated cobblestone farm setups.

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