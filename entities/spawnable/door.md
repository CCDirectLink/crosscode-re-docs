# Door
`ig.ENTITY.Door`

## Structure
inherits from [Animated Entity](/entities/base/animated-entity.md)

```ts

declare type DoorTransitionTypes = "REGULAR" | "INTER_AREA";


declare type Door = {
    "type": "Door",
    "settings": {
        "doorType": DoorType, // default: "DEFAULT"

        // condition to open
        "condition":  VarCondition,
        
        // view direction
        "dir": FACE4, // default: "SOUTH"

        // base path is assets/maps/
        "map": DotPath,

        // marker name on the specified map
        "marker": string, 

        // will become transparent if true
        "hideCondition": VarCondition,

        "blockEvent": Event,

        "blockEventCondition": VarCondition,

        // Dependent on the area-style
        // what variation of a door you can get 
        "variation": DoorVariation,
        
        "transitionType": DoorTransitionTypes,
    }
};
```

### External Type References

[DoorType](/types/door-type.md)

[VarCondition](/types/var-condition.md)

[FACE4](/types/faces/face4.md)

[DotPath](/types/dot-path.md)