# Location

This is a structure contained inside a PlayerSkins sub-object with the "Appearance" type.

# Format

```
{
 "sheet": <
  AnimationSheet index such as "player-skins.xmas" - alternatively, the AnimationSheet object can be inline
  Should be multi-dir animation sheet with:
   "shapeType": "Y_FLAT"
   "offset": { "x": 0, "y": -4, "z": 0 },
   "dirs": 8
  (In particular, the player seems to have an in-built offset that is counteracted with this one.)
 >,
 "fx": <EffectSheet index such as "skins.xmas" - alternatively, the EffectSheet object can be inline. This counts as a step effect.>,
 "gui": <
  Contains the full-body Lea menu images; full-size full-colour and smaller 'outline'.
  The filename has "media/gui/skins/" prepended to it.
  "xmas.png" is an example.
  The same layout is in "media/gui/skins/menu.png", but it's shifted to the right.
 >
}
```

