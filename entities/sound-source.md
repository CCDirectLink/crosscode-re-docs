# SoundSource
`ig.ENTITY.SoundSource`

## Structure
inherits from [entity](/entities/entity.md)


```ts

declare 
declare type SoundSource = {
    "type": "SoundSource",
    "settings": {

        // relative to CrossCode's assets folder
        "sound": RelativeURL,
        
        "volume": Number, // range: [0, 1]
                          // default: 1
        
        // Internally the playback rate (how fast to play the track)
        "speed": Number, // recommended range: [0.5, 5.0]

        // In seconds, how long to fade out 
        "fadeDuration": Number, 

        // In pixel, the radius it should be heard in
        "radius": Number, 

        // the direction of the sound range
        "rangeType": SoundRangeType,

        "spawnCondition": VarCondition
    }
};
```

### External Type References

[VarCondition](/types/var-condition.md)

[RelativeURL](/types/relative-url.md)

[SoundRangeType](/types/sound-range-type.md)