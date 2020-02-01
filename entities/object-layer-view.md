# ObjectLayerView
`ig.ENTITY.ObjectLayerView`

???

## Structure
inherits from [entity](/entities/animated-entity.md)
```ts
declare type Layer = "object1" | "object2" | "object3";

declare type EffectSheet = {
    "name": string,
    // path relative to data/effects/ 
    // folders seperators are replaced with a .
    "sheet" : string
};

declare type ObjectLayerView = {
    "type": "ObjectLayerView",
    "settings" : {
        "collType": CollisionType // default: "BLOCK"

        // this overrides the entities height
        "zHeight": Number, // default: 0

        "heightShape": HeightShape, // default: "NONE"

        "shape": CollisionShape, // default: "RECTANGLE"
        
        // has something to do with how sprites are drawn
        // playing with the number reveals it deals with
        // y axis draw order
        // Let's call it the y wall ratio
        "wallY": Number, // range: [0,1]
        
        
        // Optional fields
        "terrain": Terrain, 

        "showEffect": EffectSheet,
        "hideEffect": EffectSheet,

        // If true, will disallow navigation to take
        // place in the bounds of the entity
        "blockNavMap": boolean,

        // treated like a part of the gui 
        // pretty much draw it above the entire map
        "guiSprites": boolean,
        
        // the condition to make it transparent
        "hideCondition": VarCondition
    }
};
```
### External Type References

[CollisionType](/types/collision-type.md)

[HeightShape](/types/collision-height-shape.md)

[CollisionShape](/types/collision-shape.md)

[Terrain](/types/terrain.md)

[VarCondition](/types/var-condition.md)