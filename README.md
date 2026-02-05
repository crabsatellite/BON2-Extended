# BON2-Extended

**A fork of [BON2](https://github.com/tterrag1098/BON2) with extended MCP mappings support, modernized for Java 17+**

> **BON2** = Bearded Octo Nemesis 2, maintained by [tterrag1098](https://github.com/tterrag1098), originally rewritten by [Parker8283](https://github.com/Parker8283) from [Immibis's BON](https://github.com/immibis)

## What's Different?

This fork extends BON2 to support **all Minecraft versions using MCP mappings** (1.7.10 - 1.16.5), with modern Java compatibility and additional features.

### Key Features

| Feature              | Original BON2      | BON2-Extended                 |
| -------------------- | ------------------ | ----------------------------- |
| Java Version         | Java 8             | Java 17+                      |
| Gradle Version       | 2.9                | 8.5                           |
| MC Version Support   | Gradle cache only  | 1.7.10 - 1.16.5 (25 versions) |
| Offline Mode         | ❌ Requires mcpbot | ✅ Built-in mappings          |
| Library Download     | ❌                 | ✅ 40 common libraries        |
| CLI Mapping Download | ❌                 | ✅ `--download` command       |

## Supported Minecraft Versions

All versions using MCP mappings before Mojang official mappings (1.17+):

| Version    | Type     | Mapping Key                |
| ---------- | -------- | -------------------------- |
| **1.16.5** | Snapshot | `1.16.5-snapshot_20210309` |
| **1.16.3** | Snapshot | `1.16.3-snapshot_20201028` |
| **1.16.2** | Snapshot | `1.16.2-snapshot_20200916` |
| **1.16.1** | Snapshot | `1.16.1-snapshot_20200723` |
| **1.16**   | Snapshot | `1.16-snapshot_20200514`   |
| **1.15.1** | Snapshot | `1.15.1-snapshot_20200220` |
| **1.14.3** | Snapshot | `1.14.3-snapshot_20190719` |
| **1.14.2** | Snapshot | `1.14.2-snapshot_20190608` |
| **1.13**   | Snapshot | `1.13-snapshot_20180921`   |
| **1.12.2** | Stable   | `1.12.2-stable_39`         |
| **1.12.1** | Stable   | `1.12.1-stable_39`         |
| **1.12**   | Stable   | `1.12-stable_39`           |
| **1.11.2** | Stable   | `1.11.2-stable_32`         |
| **1.11**   | Stable   | `1.11-stable_32`           |
| **1.10.2** | Stable   | `1.10.2-stable_29`         |
| **1.10**   | Stable   | `1.10-stable_29`           |
| **1.9.4**  | Stable   | `1.9.4-stable_26`          |
| **1.9**    | Stable   | `1.9-stable_24`            |
| **1.8.9**  | Stable   | `1.8.9-stable_22`          |
| **1.8.8**  | Stable   | `1.8.8-stable_20`          |
| **1.8**    | Stable   | `1.8-stable_18`            |
| **1.7.10** | Stable   | `1.7.10-stable_12`         |

> **Note:** Minecraft 1.17+ uses Mojang official mappings and doesn't need BON2 for deobfuscation.

## Installation

### Download

Download the latest release from [Releases](https://github.com/crabsatellite/BON2-Extended/releases) or build from source.

### Build from Source

```bash
git clone https://github.com/crabsatellite/BON2-Extended.git
cd BON2-Extended
./gradlew fatJar
```

Output: `build/libs/BON-3.0.0.CUSTOM-all.jar`

## Usage

### Quick Start (CLI)

```bash
# Download mappings for your MC version first
java -jar BON-3.0.0.CUSTOM-all.jar --download --mappingsVer 1.12.2

# Deobfuscate a mod
java -jar BON-3.0.0.CUSTOM-all.jar --inputJar MyMod-1.12.2.jar --mappingsVer 1.12.2
```

### GUI Mode

```bash
java -jar BON-3.0.0.CUSTOM-all.jar
```

### CLI Commands

```bash
# List all available mappings
java -jar BON-3.0.0.CUSTOM-all.jar --list

# Download all mappings at once
java -jar BON-3.0.0.CUSTOM-all.jar --download all

# Download specific mapping
java -jar BON-3.0.0.CUSTOM-all.jar --download --mappingsVer 1.16.5-snapshot_20210309

# Deobfuscate with shorthand version
java -jar BON-3.0.0.CUSTOM-all.jar --inputJar input.jar --outputJar output.jar --mappingsVer 1.12.2

# Use custom mapping directory
java -jar BON-3.0.0.CUSTOM-all.jar --inputJar input.jar --mappingsDir ./my-mappings
```

### Library Download (for Decompilation)

After deobfuscation, you may want to decompile with CFR. Download common libraries:

```bash
# List available libraries
java -jar BON-3.0.0.CUSTOM-all.jar --list-libs

# Download all libraries
java -jar BON-3.0.0.CUSTOM-all.jar --download-libs all

# Download specific library by Maven coordinate
java -jar BON-3.0.0.CUSTOM-all.jar --download-libs --lib com.google.code.gson:gson:2.8.0
```

**40 built-in libraries** including:

- JSON: gson, jackson-core/databind/annotations, json-simple
- Apache: commons-io, commons-lang3, commons-codec, commons-compress, httpclient, httpcore, log4j
- Game: lwjgl, lwjgl_util, jinput, jutils, joml, vecmath
- Bytecode: asm, asm-commons, asm-tree, asm-analysis, asm-util
- Network: netty-all
- Utility: guava, fastutil, trove4j, icu4j, jna, jna-platform, oshi-core, jopt-simple, bcprov-jdk15on

> **Note:** Mojang libraries (authlib, patchy) are not on Maven Central. Get them from `.minecraft/libraries/com/mojang/`.

## Complete Deobfuscation + Decompilation Workflow

```bash
# 1. Download mappings
java -jar BON-3.0.0.CUSTOM-all.jar --download --mappingsVer 1.12.2

# 2. Download common libraries for decompilation
java -jar BON-3.0.0.CUSTOM-all.jar --download-libs all

# 3. Deobfuscate the mod JAR
java -jar BON-3.0.0.CUSTOM-all.jar --inputJar MyMod-1.12.2.jar --mappingsVer 1.12.2

# 4. Download CFR decompiler
curl -O https://github.com/leibnitz27/cfr/releases/download/0.152/cfr-0.152.jar

# 5. Decompile with dependencies
java -jar cfr-0.152.jar MyMod-1.12.2-deobf.jar --outputdir decompiled \
  --extraclasspath "libs/*.jar"
```

## Changes from Original BON2

### 1. Extended MCP Mappings Support

- Added 25 mapping sets covering MC 1.7.10 - 1.16.5
- All mappings downloadable from Forge Maven
- No dependency on mcpbot.bspk.rs (defunct)

### 2. Modernized Build System

- Upgraded Gradle 2.9 → 8.5
- Updated deprecated API calls
- Java 17+ compatible

### 3. New CLI Features

- `--download` - Download MCP mappings
- `--list` - List available mappings
- `--download-libs` - Download common libraries
- `--list-libs` - List available libraries

### 4. Bug Fixes

- Fixed duplicate JAR entry handling
- Fixed version parsing for `39-1.12` format
- Improved error handling

## Custom Mappings

For unsupported versions, create custom mapping files:

```
mappings/
└── 1.6.4/
    ├── fields.csv
    └── methods.csv
```

**fields.csv format:**

```csv
searge,name,side,desc
field_70170_p,worldObj,2,
```

**methods.csv format:**

```csv
searge,name,side,desc
func_70003_b,shouldExecute,2,
```

Use with: `--mappingsDir mappings/1.6.4`

## Credits

- **BON2 Maintainer**: [tterrag1098](https://github.com/tterrag1098/BON2) (primary upstream repository)
- **BON2 Original Rewrite**: [Parker8283](https://github.com/Parker8283)
- **BON (v1)**: [Immibis](https://github.com/immibis)
- **MCP Mappings**: [MCPBot Team](http://www.modcoderpack.com/)

## License

This project is licensed under **LGPL v3**, the same license as the original BON2 project.

See [LICENSE](LICENSE) for details.

---

_This fork is maintained by [@crabsatellite](https://github.com/crabsatellite/BON2-Extended) for the Minecraft modding community._
