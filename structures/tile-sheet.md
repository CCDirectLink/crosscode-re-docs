# Location

Various places, this is an internal structure.

# Description

TileSheets are used to represent an ordered set of sub-images in a grid pattern.

They are, essentially, a more complex form of reference to an image.

TileSheets are used so other formats can refer to frame numbers, rather than explicitly describe each and every frame wherever it is referenced.

Note that the coordinates described by a TileSheet may not be strictly followed.

# Format

```
{
 "src": <An image path, such as "media/entity/pets/pet-fox.png">,
 "width": <The width of each tile, as an integer>,
 "height": <The height of each tile, as an integer>,
 "xCount": <The amount of horizontal tiles, as an integer. Optional ; if not provided, guessed by dividing the image width by tile width>,
 "offX": <The base X offset of the tile grid. Optional, defaults to 0.>,
 "offY": <The base Y offset of the tile grid. Optional, defaults to 0.>
}
```
