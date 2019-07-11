# Location

This is a structure contained inside a PlayerSkins sub-object with the "Aura" type.

# Format

```
{
 "fx": <
  EffectSheet index such as "skin-aura.menacing".
  Alternatively, the EffectSheet object can be inline.
  If the relevant effect of "auraNeutral", "auraCold", "auraHeat", "auraShock", "auraWave"
   is present, that will take priority. Otherwise, the "aura" effect is used.
 >
}
```

