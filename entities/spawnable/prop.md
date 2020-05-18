# Prop
`ig.ENTITY.Prop`

## Structure
inherits from [Animated Entity](/entities/base/animated-entity.md)

```ts
declare type PropType = {
    // name of prop to use within sheet
    "name": string,

    // base path: assets/data/props/
    "sheet": DotPath
};

// name of anim in selected prop
// only works if the prop has .anims field
declare type EntityAnimation = string;

declare type ConditionAnimation = {
    "condition": VarCondition,
    "anim": EntityAnimation,
    "interact": PropInteract, // default: null
};

declare type Prop = {
    "type": "Prop",
    "settings": {
        "propType": PropType,

        "propAnim": EntityAnimation, // default: "default" 

        "condAnims": ConditionAnimations,

        "touchVar": VarName,

        "interact": PropInteract,

        "showEffect": Effect,

        "hideEffect": Effect,

        "permaEffect": Effect,

        "hideCondition": VarCondition
    }
};
```