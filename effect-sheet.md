# Location

`assets/data/effects/*.json`, or in subdirectories ("skins.xmas" is `assets/data/effects/skins/xmas.json`)

# Format

```
{
 "DOCTYPE": "EFFECT",
 "ANIMS": <
  Optional inline AnimationSheet (see animation-sheet.md),
   expected to be single-direction, with caveats:
   1. shapeType defaulting to "YZ_EXPAND"
   2. wallY defaulting to 1
   3. centerPivot defaulting to true
 >,
 "FACEANIMS": <
  Optional inline AnimationSheet (see animation-sheet.md),
   forcefully made multiple-direction.
 >,
 "EFFECTS": <
  Object.
  One property for each effect in the sheet, where the key is a string (the effect name)
   and the value is an array.
  The array contains Effect Steps, which are described in the "Effect Steps" section
 >
}
```

# EffectSpline of XType

This is a sub-component of a sub-sub-component that changes a particle's visual state.

I don't actually know the details of how this works.

It seems, conceptually, that there's a percentage value that starts at -100, and goes to 100.

"init" is at -100, "start" is at 0, and "end" is at 100.

```
 "init": <XType>,
 "start": <Optional, {"value": <XType>, "spline": <Optional, key in ig.KEY_SPLINES>}>
 "end": <Optional, {"value": <XType>, "spline": <Optional, key in ig.KEY_SPLINES>}>
```

# ig.ParticleState

This is used in EffectConfig.loadParticleData and thus in Effect Steps that use that.

```
 "pAlpha": <Optional: EffectSpline of Number>,
 "pScale": <Optional: EffectSpline of Vec2>,
 "pRotate": <Optional: EffectSpline of Number>
```

# EffectConfig.loadParticleData

This is used in Effect Steps, and implicitly adds to the step formats.

It contains ig.ParticleState, but additionally:

```
 "anim": <Optional: String name of a supplied animation>,
 "followUpAnim": <Optional: String name of a supplied animation>,
 "postAnim": <Optional: String name of a supplied animation>,
 "moveWithTarget": <Optional: Number>,
 "particleDuration": <Optional: Number>,
 "particleDurVariance": <Optional: Number>,
 "angleVary": <Optional: Number>,
 "randFlip": <Optional: Boolean>,
 "cancelable": <Optional: Boolean>,
 "pLight": <Optional: String from ig.LIGHT_SIZE>
```

# Effect Steps

An effect has a linear timeline, with potentially a looping part.

This timeline is made up of effect steps.

Effect steps, like any other kind of step, are objects that describe their type with the "type" property.

Effect steps have a duration described by the step type.

The timeline's loop markers are placed with the "LOOP\_START" and "LOOP\_END" steps, which have no additional properties.

Note that most effect steps aren't described here, only the basics, as the later effect steps are rather insanely complicated.

## WAIT

The "WAIT" effect step has the format:

```
{
 "type": "WAIT",
 "time": <Number, time in seconds>
}
```

The duration of the step is described by the given time. It otherwise performs no action.

## LOOP_START / LOOP_END

The "LOOP\_START" effect step is just `{"type": "LOOP_START"}` with no additional parameters.

The "LOOP\_END" effect step is just `{"type": "LOOP_END"}` with no additional parameters.

They're markers to control the looping, but perform no actions and have zero duration.

## PLAY_ANIM

This is an example of the incredibly complicated EffectConfig.loadParticleData usage.

The properties it can call it's own are:

```
 "type": "PLAY_ANIM",
 "useTargetAngle": <Boolean>,
 "keepAngleSync": <Boolean>,
 "offset": <Vec3>,
 "rotOffset": <Vec3>
```

The rest are EffectConfig.loadParticleData's various fields, and so on.


