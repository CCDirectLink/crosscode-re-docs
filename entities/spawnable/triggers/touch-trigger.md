# TouchTrigger
`ig.ENTITY.TouchTrigger`

## Structure
inherits from [Entity](/entities/base/entity.md)

```ts

declare type TouchTrigger = {
    "type": "TouchTrigger",
    "settings": {
        "startCondition": VarCondition, // default: "true"
        "variable": VarName,
        "type": TouchTriggerType, // default: "SET_TRUE"
        
        // this overrides the entities height
        "zHeight" : Number,

        "shape": CollisionShape,
        
        // if true, then party members can trigger it
        "reactToParty": boolean
    }
};

```

### External Type References

[VarCondition](/types/var-condition.md)

[VarName](/types/var-name.md)

[CollisionShape](/types/collision-shape.md)

[TouchTriggerType](/types/touch-trigger-type.md)