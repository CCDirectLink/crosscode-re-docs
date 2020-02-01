# Entity
`ig.Entity`

This is the bare bone structure for any Entity types.

## Structure

```ts
declare type LevelObject = {
    "offset": Number,
    "level": Integer
};

declare type Level = Integer | LevelObject;

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

# Notes

Should not directly spawn this.

### External Type References

[VarCondition](/types/var-condition.md)

