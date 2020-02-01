# Marker
`ig.ENTITY.Marker`

This is used for spawning the player on a specific spot on a map.


## Structure

inherits from [Entity](/entities/base/entity.md)
```ts

declare type FACE4 = "NORTH" | "EAST" | "SOUTH" | "WEST";

declare type Marker = {
    "type" : "Marker",
    "settings" : {
        // mandatory fields
        "name": string,

        // optional fields
        "dir": FACE4 // default: "NORTH"

        // constant fields
        "size": {
            "x": 32,
            "y": 32,
            "z": 0
        }
    }
};
```


### External Type References

[FACE4](/types/faces/face4.md)

## Notes

There is no collision so the player can not run into.