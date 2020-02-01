# Door
`ig.ENTITY.Door`

## Structure
inherits from [Animated Entity](/entities/base/animated-entity.md)

```ts

declare type Door = {
    "type": "Door",
    "settings": {

        "doorType": DoorType, // default: "DEFAULT"

        // condition to open
        "condition":  VarCondition,
        
        // view direction
        // set to SOUTH if the doorType has hardcoded anims
        "dir": FACE4, // default: "SOUTH"

        // base path is assets/maps/
        "map": DotPath,

        // marker name on the specified map
        "marker": string, 

        // will become transparent if true
        "hideCondition": VarCondition,



        // event to play if player enters door and 
        // blockEvenCondition evaluates to true
        "blockEvent": Event,

        "blockEventCondition": VarCondition,

        // Dependent on the mapStyle
        // what variation of a door you can get 
        // ignored if the doorType has hardcoded anims
        "variation": DoorVariation,
        
        "transitionType": DoorTransitionType,
    }
};
```

### External Type References

[DoorType](/types/door/types.md)

[VarCondition](/types/var-condition.md)

[FACE4](/types/faces/face4.md)

[DotPath](/types/dot-path.md)

[DoorTransitionType](/types/door/transition-types.md)