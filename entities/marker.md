# Marker
`ig.ENTITY.Marker`

This is used for spawning the player on a specific spot on a map.


## Structure

inherits from [entity](/entities/entity.md)
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


## Notes

There is no collision so the player can not run into.