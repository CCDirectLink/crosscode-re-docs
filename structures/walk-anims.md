# Location

WalkAnims are part of the 'common base' used by all Actors.

# Format

Most of these animations have fallbacks in various situations - only idle is truly required. As the logic is complicated: `ig.ActorEntity.update` has further details.

The strings all refer to animation names within a related AnimationSheet.

Be warned that this file does not cover every animation every NPC has.

Most instances use specific IDs - WalkAnims only configure the more generic code shared between NPC runners, the player, etc.

```
{
 "idle": <String. "Optional", but not really - avoiding this will more or less disable WalkAnim processing. (useful if you want that)>
 "preMove": <String. Optional>
 "move": <String. Optional, but if you're using walk animations you probably want to include this one>
 "moveRev": <String. Optional>
 "moveLeft": <String. Optional>
 "run": <String. Optional, but if you're using walk animations you should include this if you include move, otherwise movement speeds won't look right>
 "runRev": <String. Optional>
 "runLeft": <String. Optional>
 "brake": <String. Optional>
 "preIdle": <String. Optional>
 "jump": <String. Optional>
 "fall": <String. Optional>
 "hover": <String. Optional>
 "preHoverMove": <String. Optional>
 "hoverMove": <String. Optional>
 "hoverMoveRev": <String. Optional>
 "land": <String. Optional>
}
```


