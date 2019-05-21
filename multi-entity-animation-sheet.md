# Location

Same as other kinds of AnimationSheet.

# Overview

A `MULTI_ENTITY_ANIMATION` is used for extremely complex animated objects.

It appears to effectively act as the entity's full 3D "model" in CrossCode.

As with other kinds of AnimationSheet, it contains a "namedSheets" key.

However, the format itself is more rigidly defined, which may help in understanding it.

# Format

```
{
 "DOCTYPE": "MULTI_ENTITY_ANIMATION",
 "namedSheets": <
  This is copied to the individual part AnimationSheets.
  Object with string keys (sheet names) and TileSheet values. See structures/tile-sheet.md for details on that.
 >,
 "baseSize": <Vec3>,
 "parts": <
  Object with string keys (part names) and values of the form:
  {
   "group": <String>,
   "persistAnim": <Boolean, possibly optional>,
   "collType": <Optional String (a ig.COLLTYPE), defaults to "BLOCK">,
   "heightShape": <Optional String (a ig.COLL_HEIGHT_SHAPE), defaults to "NONE">,
   "pos": <Vec3>,
   "size": <Vec3>,
   "padding": <Optional Vec2>,
   "anims": <Inline AnimationSheet describing part animations. Note that namedSheets is overwritten with the root's namedSheets>
  }
 >,
 "anims": <
  Object with string keys (animation names) and MultiEntityAnimation values.
  This is where the actual animations are (the per-part animations are controlled here.)
 >
}
```

It is important to clarify that from experimentation, I've determined the AABB starts at pos and extends for size.

# MultiEntityAnimation

This is a sub-object that needs its own section to break down the complexity.

This is how a 3D movement is created as a whole.

```
{
 "time": <Number - seconds per frame>,
 "frameCount": <The amount of frames>,
 "repeat": <Optional boolean defaulting to True>,
 "anchor": <Optional Vec3>,
 "flipDir": <Optional String (a ig.MULTI_ANIM_FLIP), defaults to "NONE">,
 "partAnims": <
  Object with part names as keys, and as values, the animation controls for individual parts, which take the form of:
  {
   posFrames: <Array of triplets of numbers (similar to Animation's frame offset array) - the length of this is thus frameCount * 3>,
   anim: <String - an animation that exists in that part to play>,
   reset: <Boolean. If true, rewinds the animation before playing it - given the related internal "synced" flag, this is for maintaining sync between the sub-animation and the wider-scale animation>,
   collType: <Optional String (a ig.COLLTYPE), defaults to resetting it>
  }
 >
}
```

Additionally, you may find "customAnim" as a key in PartAnims.

The engine does not interpret this, and I assume it to be created and maintained by the development environment.

Such cases also contain anim names in the parts of the form `_custom_idle`.

# Examples

None in this repository, but `assets/data/animations/boss/cargo-crab.json` from the game may be helpful.

