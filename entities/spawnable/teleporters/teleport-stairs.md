# TeleportStairs
`ig.ENTITY.TeleportStairs`


## Structure
inherits from [Entity](/entities/base/entity.md)

```ts
declare type StairType = "UPWARDS_EAST" | "UPWARDS_WEST" | "DOWNWARDS_EAST" | "DOWNWARDS_WEST";

declare type TeleportStairs = {
    "type": "TeleportStairs",
    "settings": {
        "stairType": StairType,
        
        // base path is assets/maps/
        "map": DotPath,

        // marker name on the specified map
        "marker": string,


        // event to play if player enters door and 
        // blockEvenCondition evaluates to true
        "blockEvent": Event,

        "blockEventCondition": VarCondition,

        // probability they will enter or leave from this
        "npcRunnerProb": Number, // range: [0, 1]

        "layer": ObjectLayer,

        "transitionType": DoorTransitionType
    }
};
```


### External Type References

[ObjectLayer](/types/object-layer.md)

[DoorTransitionType](/types/door/transition-types.md)