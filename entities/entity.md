# Entity
`ig.Entity`

This is the bare bone structure for any Entity types.

## Structure
> Note: You can not spawn an entity by itself

```ts
declare type LevelObject = {
    "offset": Number,
    "level": Integer
};

declare type Level = Integer | LevelObject;

// need to write explanation as to what can be done
declare type VarCondition = string;

declare type Entity = {
    "x": Integer,
    "y": Integer,
    "level": Level,
    // optional elements
    "settings": {
        "mapId": Integer,
        "name": string,
        "size": Vec3

        // any entity could have a spawn condition
        "spawnCondition": VarCondition
    }
}
```

### External Type References

[VarCondition](/types/var-condition.md)