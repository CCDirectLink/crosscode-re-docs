# HiddenBlock
`ig.ENTITY.HiddenBlock`

## Structure
inherits from [Entity](/entities/base/entity.md)
```ts

declare type HiddenBlock = {
    "type": "HiddenBlock",
    "settings" : {

        "shape": CollisionShape, // default: "RECTANGLE"
        
        "heightShape": HeightShape, // default: "NONE"

        // this overrides the entities height
        "zHeight": Number, // default: 0


        "collType": CollisionType // default: "BLOCK"

        // Optional fields
        "terrain": Terrain
    }
};
```
### External Type References

[CollisionShape](/types/collision-shape.md)

[HeightShape](/types/collision-height-shape.md)


[CollisionType](/types/collision-type.md)

[Terrain](/types/terrain.md)

# Notes

Usually used for an intermediate step stone to another height, e.g stairs.