# GlowingGround
`ig.ENTITY.GlowingGround`

## Structure
inherits from [Entity](/entities/base/entity.md)

```ts
declare type GlowingGround = {
    "type": "GlowingGround",
    "settings": {
        
        // css color
        "color1": string,


        // css color
        "color2": string,

        // time it takes to turn from color1 to color2 and vice versa.
        "duration": Number, // default: 1

        // default value
        "size": {
            "x": 32,
            "y": 32,
            "z": 0
        }
    }
};

```