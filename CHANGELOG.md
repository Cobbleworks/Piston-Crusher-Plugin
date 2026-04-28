# Changelog

All notable changes to Piston Crusher will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

## [1.0.1] - 2026-04-28

Piston Crusher v1.0.1 delivers stability improvements and maintenance fixes following the initial release.

### Stability And Maintenance

- **Runtime Safety**: Improved handling of edge-case piston interactions
- **General Refinements**: Applied maintenance updates for long-running servers

**Note:** If you encounter any bugs or issues, please don't hesitate to open an [issue](https://github.com/Cobbleworks/Piston-Crusher-Plugin/issues). For any questions or to start a discussion, feel free to initiate a [discussion](https://github.com/Cobbleworks/Piston-Crusher-Plugin/discussions) on the GitHub repository.

## [1.0.0] - 2026-04-01

Piston Crusher v1.0.0 is the initial release, delivering configurable piston-driven block crushing with runtime whitelist and multiplier management and persistent settings.

### Crushing Mechanics

- **Piston-Driven Crushing**: Whitelisted blocks pushed into the configured crusher block are destroyed and drop items at the configured multiplier
- **Configurable Crusher Block**: Choose the target block type that acts as the crusher via `/pistoncrusher setcrusherblock`
- **Drop Multiplier**: Set a global drop multiplier (minimum 1.0) via `/pistoncrusher multiplier`

### Administration

- **Runtime Whitelist Management**: Add, remove, and list whitelisted materials via `/pistoncrusher whitelist add|remove|list` without restarting
- **Persistent Settings**: Whitelist and crusher block configuration saved in `whitelist.yml` and `crusherblock.yml`
- **Tab Completion**: Subcommands and material names are suggested automatically

**Note:** If you encounter any bugs or issues, please don't hesitate to open an [issue](https://github.com/Cobbleworks/Piston-Crusher-Plugin/issues). For any questions or to start a discussion, feel free to initiate a [discussion](https://github.com/Cobbleworks/Piston-Crusher-Plugin/discussions) on the GitHub repository.
