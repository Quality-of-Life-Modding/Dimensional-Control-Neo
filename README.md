# Dimensional Control Neo
Previously called **Dimensional Structure Restrict (DimStructRestrict)**.

Dimensional Control Neo is a lightweight Minecraft Forge mod for **Minecraft 1.20.1** that lets you control worldgen and other content behavior by dimension-scoped rules.

---

## Credits

- **Troy Cook** ([@cookta2012](https://github.com/cookta2012)) — original mod author and maintainer.
- **Matt** (`matt/dimensionalcontrol`) — core rewrite/backport contributions that this branch builds on.

---

## Features

- Dimension-scoped rule definitions.
- Rule categories currently supported in config:
  - `dimensions`
  - `structures`
  - `structurePoolElements`
  - `features`
  - `entities`
  - `loot`
- `whitelist` / `blacklist` modes.
- Optional `always_report_success` flag (legacy `false_place` key is still accepted for backward compatibility).
- Expanded resolved output is written for debugging.

---

## Configuration

Primary config path:

```text
<minecraft_root>/config/dimensionalcontrolneo/definitions.json
```

Expanded/debug output path:

```text
<minecraft_root>/config/dimensionalcontrolneo/expanded-definitions.json
```

If `definitions.json` does not exist, the mod generates a starter template.

---

## `definitions.json` shape

```jsonc
{
  "dimensions": [
    {
      "dimension": "minecraft:overworld",
      "whitelist": [],
      "always_report_success": false,
      "active": true
    }
  ],
  "structures": [
    {
      "dimension": "minecraft:overworld",
      "whitelist": ["minecraft:village_plains"],
      "always_report_success": false,
      "active": true
    }
  ],
  "structurePoolElements": [
    {
      "dimension": "minecraft:overworld",
      "blacklist": ["minecraft:empty"],
      "active": true
    }
  ],
  "features": [
    {
      "dimension": "minecraft:overworld",
      "blacklist": ["minecraft:lake_lava_underground"],
      "active": true
    }
  ],
  "entities": [
    {
      "dimension": "minecraft:.+",
      "whitelist": [],
      "active": true
    }
  ],
  "loot": [
    {
      "dimension": "minecraft:.+",
      "blacklist": [],
      "active": true
    }
  ]
}
```

Notes:
- Exactly one of `whitelist` or `blacklist` should be present on a rule.
- `active` defaults to `false` if omitted.
- `always_report_success` defaults to `false` if omitted.
- Legacy `false_place` is read as an alias for `always_report_success`.

---

## Rule semantics

- **Structure rules are checked first**.
- If no structure-specific rule applies, **dimension rule fallback** is used.
- Rules can be disabled without removing them by setting `active: false`.

---

## Build

Use Java 17:

```bash
./gradlew build
```

---

## License

MIT License.
