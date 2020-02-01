# Collision Types
`ig.COLLTYPE`

### Values
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

It is most closely used for setting `ig.CollEntry.type`


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


COLLIDES WITH column represents the entity collision type
The remaining fields in the first row represent what is being collided into.
Each check means that the combination will acknowledge the collision.
For example, PROJECTILEs can collide with PBLOCKs. PROJECTILEs will go through other PROJECTILES.


# Value Usages

Note: Not exhaustive and might not be 100% because special cases are scattered all around the code

## NONE

When it is necessary for an entity to not collide with another entity. Collison tiles are also ignored. 

This is pretty much noclip.

Slope collisions are still recognized.


## IGNORE

idk

## PROJECTILE

The name should be self explanatory.


## VIRTUAL

By default, the player is set to this. 

## PBLOCK

Projectile Block. This collides with PROJECTILEs.

## NPBLOCK

Non projectile block. This collides with almost everything but PROJECTILEs.

## BLOCK

Just blocks almost everything.

## TRIGGER

Functionally similar to NONE. Used to indicate something special will happen on collision. 

## PASSIVE

Used by particles.


## SEMI_IGNORE

Used by PartyMembers.

## FENCE

Name is self explanatory.

## NPFENCE

Like fence, but does not block Projectiles.