# Location

`assets/data/animations/*.json`, or in subdirectories ("pets.shiba" is `assets/data/animations/pets/shiba.json`)

# Format Notes

The AnimationSheet 'format' is actually 3 separate formats:

Single-dir-animations, `MULTI_DIR_ANIMATION`, and `MULTI_ENTITY_ANIMATION`.

Single-dir-animations don't have a DOCTYPE. See ig.RainDropEntity for how this works.

An example of `MULTI_ENTITY_ANIMATION` is `assets/data/animations/boss/antlion.json`.

It appears to effectively act as the entity's full 3D "model" in CrossCode.

Understanding and editing those is probably going to be incredibly painful with or without an editor.

Only `MULTI_DIR_ANIMATION` is described here for now.

However, much of what applies here partially applies to single-dir animation sets.

Note that this documentation is likely to be incomplete.

In particular, there is some evidence to suggest multiple animations with the same name cause some form of appending.

(`sc.TESLA_COIL_TYPE.SOURCE_LOOSE` is an example - see the "charge" name.)

# Directions

CrossCode supports the following direction counts:

1, 2, 4, 6, 8, and 16.

A rough reference on what the directions mean is provided in `ig.getDirectionVel`, but you may need graphing paper.

# Format Notes for Single-Dir and Multi-Dir Animations

The Single-Dir and Multi-Dir AnimationSheet types are recursive structures. They contain structures with the same format as themselves.

This is used as a way of reducing the amount of copy & pasted text.

Fields which aren't specified in a sub-structure default to the value in the parent structure.

There are certain root-level elements that do not have effects in sub-structures, and those will be described in the usual manner.

The `SUB` property contains an array of objects which inherit properties from the 'parent' object.

(Note, however, that the `name` and `SUB` properties are not inherited.)

Elements with the `name` property (keeping in mind that property is not inherited) create the actual \*AnimationSet instances.

# Format (MULTI_DIR_ANIMATION)

The root-level elements for MULTI\_DIR\_ANIMATION are as follows:

```
{
 "DOCTYPE": "MULTI_DIR_ANIMATION",
 "namedSheets": {
  <Entries with string properties and TileSheet values. See structures/tile-sheet.md for details on that.>
 }
}
```

Following that format does create a technically valid file, but said file does not contain any animations.

As for the effects of 'name':

A MultiDirAnimationSet instance is responsible for a single animation across the different directions that animation supports.

(A single MultiDirAnimationSet instance has multiple `ig.Animation` instances - one per supported direction.)

These firstly use the following properties (via inheritance or otherwise):

```
{
 "dirs": <An integer, or a string with an integer written in it due to JavaScript type weirdness>,
 "sheet": <Some sort of sheet reference to pass to ig.Animation - can be a string or a TileSheet>,
 "anchorOffsetX": <number, array with one entry per direction, or not present>,
 "anchorOffsetY": <number, array with one entry per direction, or not present>,
 "anchorOffsetZ": <number, array with one entry per direction, or not present>
}
```

Then, the animation can contain either a `frames` array, a `dirFrames` array, or neither.

For a `frames` array, the additional format is as follows (note that this is still properties being included in the same object):

```
{
 "frames": <An array for an Animation frames list, that is, one tile index for each frame. -1 means 'invisible' - this is not affected by frame tile indexing.>,
 "tileOffsets": <An array. For each direction, an integer that offsets the frame tile indexes>,
 "flipX": <Optional: An array, containing, for each direction, a value coerced to a boolean for that direction>,
 "dirOffsets": <Optional: An array containing Vec3s. These are added to the "offset" property (created if it doesn't exist).>,
 "dirAngles": <Optional: An array containing numbers. The "angle" property for each direction is overwritten with values from here.>,
 "allDirFlipX": <Optional: Applied after flipX, inverts flipX values. If none exist, applies flipX to everything.>
}
```

Further details are based on the Animation format. See "animation.md" for details on this.

For a `dirFrames` array, the additional format is as follows (note that this is still properties being included in the same object):

```
{
 "dirFrames": [ <One array for each direction, in turn each individually being a valid 'frames' array)> ],
 "flipX": [ <One value, which is coerced to boolean, for each direction> ]
}
```

...and any further details are based on the Animation format.

Note that, as stated before, there is some conversion, so where fields seem to overlap, or fields described in the Animation format document don't work, it's likely that's what's going on.

# Note On Actual Structures

Actual CrossCode Multi-Dir AnimationSheets seem to use a structure made up of three levels.

There's the root level, which contains the namedSheets and possibly some defaults.

There's the "sheet" level, which splits the animations into their respective sheets.

And there's the "animation" level, which contains just the animation-specific data.

For editor compatibility purposes, it would be best if this structure were followed as rigidly as possible.

Otherwise, the flexibility of the format may require a perfectly compatible editor to essentially be a JSON editor with a preview box.

# Examples

If examples are made, see playerskins/appearance.md and playerskins/pet.md for further details.
