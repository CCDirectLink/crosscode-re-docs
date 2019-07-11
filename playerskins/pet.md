# Location

This is a structure contained inside a PlayerSkins sub-object with the "Pet" type.

# Format

```
{
 "animSheet": <
  AnimationSheet index such as "pets.fox", or the AnimationSheet object inline
  Should be multi-dir animation sheet with:
   "shapeType": "Y_FLAT"
   "offset": { "x": 0, "y": -1, "z": 0 },
   "gfxOffset": { "x": 0, "y": 1 },
   "dirs": 8
   (In particular, the offset prevents visual glitches near certain objects.
    Note that the offset uses -1, not -4 ; -4 is for players.
    The offset by itself fixes Z order but misaligns things, so gfxOffset corrects it.)
 >,
 "walkAnims": <WalkAnims object - see structures/walk-anims.md>,
 "actorConfig": <Optional: ActorConfig object - see structures/actor-config.md>,
 "petOffsets": <Optional: An array of Vec2s, which overrides the offsets the pet can be petted from>
}
```

Additionally, on top of the animations specified via walkAnims, the game will look for animations "idleSpecial1", "idleSpecial2", etc.

The numbering starts from 1.

The pet will use these in a similar way to Lea performing "idleStretch" when idle.

# Examples

`playerskins/pet-example/pet-example.json` contains an example Pet.

