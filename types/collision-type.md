# Collision Types

These are the valid options for `ig.CollEntry.type`

- NONE
- IGNORE
- PROJECTILE
- VIRTUAL
- PBLOCK
- NPBLOCK
- BLOCK
- TRIGGER
- PASSIVE
- SEMI_IGNORE
- FENCE
- NPFENCE

|COLLIDES WITH|     NONE    |    IGNORE   |  PROJECTILE |   VIRTUAL   |    PBLOCK   |   NPBLOCK   |    BLOCK    |   TRIGGER   |   PASSIVE   | SEMI_IGNORE |    FENCE    |   NPFENCE   |
|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|
|     NONE    |             |             |             |             |             |             |             |             |             |             |             |             |
|    IGNORE   |             |             |             |             |             |      ✓      |      ✓      |             |             |             |      ✓      |      ✓      |
|  PROJECTILE |             |             |             |             |      ✓      |             |      ✓      |             |             |             |      ✓      |             |
|   VIRTUAL   |             |             |             |      ✓      |             |      ✓      |      ✓      |             |             |             |      ✓      |      ✓      |
|    PBLOCK   |             |             |      ✓      |             |      ✓      |             |      ✓      |             |             |             |      ✓      |             |
|   NPBLOCK   |             |      ✓      |             |      ✓      |             |             |      ✓      |             |             |             |      ✓      |      ✓      |
|    BLOCK    |             |      ✓      |      ✓      |      ✓      |      ✓      |      ✓      |      ✓      |             |             |      ✓      |      ✓      |      ✓      |
|   TRIGGER   |             |             |             |             |             |             |             |             |             |             |             |             |
|   PASSIVE   |             |             |             |             |             |             |      ✓      |             |             |             |             |             |
| SEMI_IGNORE |             |             |             |             |             |      ✓      |      ✓      |             |             |             |      ✓      |      ✓      |
|    FENCE    |             |      ✓      |      ✓      |      ✓      |      ✓      |      ✓      |      ✓      |             |             |      ✓      |      ✓      |      ✓      |
|   NPFENCE   |             |      ✓      |             |      ✓      |      ✓      |      ✓      |      ✓      |             |             |      ✓      |      ✓      |      ✓      |