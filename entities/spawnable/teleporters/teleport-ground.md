# TeleportGround
`ig.ENTITY.TeleportGround`

## Structure
inherits from [Entity](/entities/base/entity.md)

```ts

declare type TeleportGround = {
    "type": "TeleportGround",
    "settings": {

        // this overrides size.z
        "zHeight": Number,

        "size": {
            // default values
            "x": 8,
            "y": 8,
            "z": 64
        },

        // view direction of the entity when interacting
        // with the teleport ground 
        "dir": FACE4,

        // base path is assets/maps/
        "map": DotPath,

        // marker name on the specified map
        "marker": string, 

        // how far away from the teleporter
        // to spawn entity
        "spawnDistance": Number, // default: 48

        // event to play if player enters door and 
        // blockEvenCondition evaluates to true
        "blockEvent": Event,

        "blockEventCondition": VarCondition,

        "transitionType": DoorTransitionType,

        // probability they will enter and leave from this
        "npcRunnerProb": Number, // range: [0, 1]

        // If true, will always walk through center of opening
        "centerWalkThrough": boolean,

    }

};
```