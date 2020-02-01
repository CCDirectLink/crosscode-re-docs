# HiddenSkyBlock
`ig.ENTITY.HiddenSkyBlock`

## Structure
inherits from [Entity](/entities/base/entity.md)
```ts

// What ever z-position is put, the actual z position will be
// 1000 less 
declare type HiddenSkyBlock = {
    "type": "HiddenSkyBlock",
    "settings" : {

        "shape": CollisionShape, // default: "RECTANGLE"

        "collType": CollisionType // default: "BLOCK"

        "size": {
            // these are the defaults
            "x": 32,
            "y": 32,
            // this is constant
            "z": 2000
        }
    }
};
```
### External Type References

[CollisionShape](/types/collision-shape.md)

[CollisionType](/types/collision-type.md)

## Notes

This is used to block off a section of an area or passageway. Not too sure the reason for existence. 
Probably used to block off some area in a multilevel map.