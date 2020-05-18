# Base (ig.Game.draw())

The entire game rendering procedure is in ig.Game.draw().
The rendering context of the canvas is in ig.system.context, but some
rendering procedure actually override it to implement effects.


It does the following:

- Calculate the relative position in which maps should be drawn,
  which is mainly useful for parallax map backgrounds (e.g. the view
  of Rookie Harbor in Rhombus square) (ig.ChunkedMap.setScreenPos())
  or true parallax maps (ig.MAP.MovingParallax.setScreenPos() overrides).
- Call the preDraw hooks. The game defines two of them:
    * ig.Light (preDrawOrder = 0) uses them to render lights (conditional lights only ?)
      using ig.game.renderer.drawLight()
    * ig.ScreenBlur (preDrawOrder = 10³), when active, use it to redirect
      ig.system.context to an offscreen canvas.
- Iterate over all visible entities (ig.game.shownEntities) and
  calculate two arrays of ig.Renderer2d.SpriteDrawSlot objects describing how
  to draw them (see ig.Renderer2d.prepareDraw()).
- Draw maps and non-gui entities (see ig.Renderer2d.drawLayers())
- Call the midDraw hooks. The game defines those:
    * ig.Light (midDrawOrder = 0) for light stuff, again.
    * ig.Weather (midDrawOrder = 100) draws the weather.
    * ig.EnvParticles (midDrawOrder = 101) draws particles
- Draw the GUI sprites (ig.Renderer2d.drawPostLayerSprites). These are e.g.
  xeno dialogs and most effects, which are drawn above everything else, like
  the player's sweeps.
- Call the postDraw hooks. The game defines those:
    * ig.ScreenBlur (postDrawOrder = 200) restores ig.system.context and
      draws the offscreen canvas at various zoom levels varying over time.
      An effect that can be seen on the very beginning of chapter 1.
    * ig.Gui (postDrawOrder = 500) which draws all the GUIs, including menus,
      HUDs, dialogs, but also the player and ennemies' HP bars.

# Maps

There are three kind of maps relevant for rendering:

- ig.MAP.Background
- ig.MAP.MovingParallax (inherits from ig.MAP.Background)
- ig.MAP.Light

Because rendering is slow, they all inherit from ig.ChunkedMap, which prerenders
the tiles into chunks, unlike the other MAP types (ig.MAP.Collision,
 ig.MAP.Navigation and ig.MAP.HeightMap which inherits from ig.Map)


# Entities

## ig.Renderer2d

This is the class that draws entities.

### prepareDraw()

This function is in charge of :

- Clipping drawn entities to the screen (unless entity.coll.alwaysRender is set)
- Sorting out gui sprites from non-gui sprites.
- Determining if a sprite has a wall part, a ground part, or both.
- Updating a sprite's `renderData.wall` or `renderData.ground` members
  (of type ig.Renderer2d.SpriteDrawSlot) with how the sprite should be drawn.
- Create a spriteSlots array for non-gui sprites and guiSpriteSlots for
  gui sprites, and sort them by the order in which sprites should
  be drawn (basically, draw sprites with a lower y coordinate first, so that
  sprites with higher y coordinate will be drawn above them).
- Preparing modified image fragments or pre-rendering some sprites.

More specifically, for each of an entity's visible sprites, it will :

- Call its updateSprites() method (animation stuff ?)
- Determine if the sprite has a wall part, a ground part, or both,
  and calculate the sprite's `renderData.wall` or `renderData.ground`
  fields (of type ig.Renderer2d.SpriteDrawSlot).
- Calculate each part's `yIndex` attribute, which will determine the draw order.
  Objects with a higher yIndex coordinate will be drawn above the others.
  The actual calculation is done by `ig.Render2d.update()`.
- Add them to the spriteSlots or guiSpriteSlots array.
- If the sprite has a `overlay.color` or `lighterOverlay.color` property,
  then create a modified image (ImageModFragment) where non-transparent pixels
  of the sprite are filled with `overlay.color` or `lighterOverlay.color`.

Then, the spriteSlots and guiSpriteSlots arrays are sorted by ascending `yIndex`
with a stable sort algorithm (Basically, the order in which sprites were
encountered is stored in each SpriteDrawSlot's `spriteIdx` index, which is used
 to break ties when two `yIndex` are equal).

### drawLayers()

Maps, sprites and their shadows are drawn using `ig.system.context` here.
GUI sprites are not drawn here.

The renderer works by iterating over the maps height levels and draw
horizontal slices of the environment.

If e.g. a map has three levels (their `height` attribute) at 0, 32 and 64,
then the game will draw :

- All entities in the slice where -9999999 (actual value) <= z <= 0
- maps and entites in the slice where 0 <= z <= 32
- maps and entites in the slice where 32 <= z <= 64
- maps and entities in the slice where 64 <= z <= 99999999 (actual value).

The draw order for a slice is the following:
- The animated tiles of maps are drawn first.
  (`ig.MAP.Background.drawAnimated()`)
- The non-animated tiles of maps are drawn afterward. (`ig.ChunkedMap.draw()`)

- Entities's sprites are then drawn by `drawEntities()` as follows:
  - Ground sprites where z is exactly the minimum z value are drawn in the
    order where they are encountered in the spriteSlots array.
-   Then the other sprites, in the order they were sorted in the spriteSlots
    array.  If a sprite is at the boundary between z levels, then it is clipped
    and only the part present in the slice is drawn.
    Shadows are drawn before their sprites.
    Each sprite is actually drawn by calling
    `ig.Renderer2d.SpriteDrawSlot.draw(minimum z, maximum z)`

## ig.Renderer2d.SpriteDrawSlot

This is an object that represent how to draw a sprite.  There are actually
up to two SpriteDrawSlot for a single sprite. This depends on whether
the sprite has a "ground" part, a "wall" part or both. To understand them,
remember that despite the "spherical" name, the game mainly deals with cubes.

Let's me illustrate with a pushable box. It has only one sprite, which
contains both the top of the cube and its wall:

```
   ┌───────┐   ┐
   │   ^   │   │
   │       │   │
   │<     >│   │ "ground" part
   │       │   │
   │   v   │   │
   ├───────┤   ┘  ┐     <─── yIndex of ground part
   │       │      │
   │       │      │
   │       │      │
   │       │      │ "wall" part
   │       │      │
   └───────┘      ┘    <─── yIndex of wall part
```

Now, this simple case assumed that wallY was zero, in which case the ground
part has height `size.y` and the wall part has height `size.z`, and
`yIndex` (which controls if the sprite is drawn above or below other sprites)
is set to the "bottom" of the sprite.

If wallY is not zero, then the thing being drawn isn't really a cube.
Basically, the "wall" part's Y coordinate is shifted by `-wallY`
and the ground part is amputated by `wallY`.

Let's look at a regular tree instead, where wallY would be set to
half of `size.y` (note that the `wallY` seen in data files is actually a
percentage relative to `size.y`, so `wallY: 0.5` in json means "set wallY to
half of `size.y`")

```
                               ┐
                     ********  │ ground part : size.y - wallY
                     ********  ┘┐
                     ********   │
                     ********   │ wall part: size.z + wallY
                        ||      │
                        ||      │          /__ yIndex
                ┌       ||      │          \   of ground part
         size.y │   A  /||\     │    /__ yIndex
 wallY┌         │   B  \  /     │    \   of wall part
      └         └       \/      ┘
```

wallY is not only used to shift the wall, it also influences the draw order,
by shifting the position of yIndex.  An object at position A will be drawn
behind the wall part, while an object at position B will be drawn above it.

For now, the actual rules to determine if an object has a wall part or
a ground part will make sense to you:

- A sprite has a wall part if its size.z is non-zero, or if wallY is above 0.
- A sprite has a ground part if its size.y is non-zero and if its wallY is
  below size.y.

If a sprite's `mergeTop` attribute is set, then the ground part is removed and
the wall part is set up to draw both parts.

### Fields

* cubeSprite : the actual sprite.
  (sprite.renderData[sometype].cubeSprite == sprite
   if sprite.renderData[sometype] exists)
* ground : True for ground parts. false for wall parts.
* yIndex : store the drawing order of the sprite.
* spriteIdx : store the current iteration count of the loop. used to
  disambiguate sprites with same yIndex.
* zMin : the z coordinate of the bottom of the sprite
* zMax : the z coordinate of the top of the sprite.
* drawShadow : whether to draw a shadow on the sprite.  Only done if the
  sprite is a wall and non-ground sprite. The actual shadow parameters
  are in cubeSprite.


### update(sprite)

This calculates the `yIndex`, `zMin` and `zMax` field. `zMin` and `zMax` are
used by `drawEntities()` to clip the sprite, while `yIndex` is used to calculate
which sprite is on top of which other sprite.

For wall parts, it is the Y coordinate of the 'bottom' of the sprite.
(`sprite.pos.y + sprite.tmpOffset.y + sprite.size.y - sprite.wallY`)
This is the position of the highest `y` coordinate occupied by the object,
subtracted by `wallY`.
wallY is thus used to shift the depth perception of the wall by fudging
the draw order.

For ground sprites, this is simply the lowest `y` coordinate occupied by
the sprite (`sprite.pos.y + sprite.tmpOffset.y`)

For gui sprites (e.g. interact icons), it is set to it's Z coordinate.
Most gui sprites's z coordinate are actually unrelated to the Z coordinate
of the map.

### draw(zMin, zMax)

Draws the non-gui sprites on ig.system.context, but only the part of the sprite
between zMin and zMax.

This mainly uses the `cubeSprite` property to get the rendering parameters.
`cubeSprite` is abbreviated as `cs` below.

The following parameters affects the rendering:

- `cs.src` is used to influence which part of the source image is drawn.
- `cs.renderMode` changes the canvas composite operation.  If `null`, then
  the default rendering mode is used.  The game often uses the `lighter`
  render mode for effects.
- `cs.pos`, `cs.tmpOffset` and `cs.gfxOffset` affects where the
  sprite will be drawn on the screen.
  The sprite will be drawn at position
  X = `cs.pos.x + cs.tmpOffset.x + cs.gfxOffset.x`
  Y = `(cs.pos.y + cs.tmpOffset.y) - (cs.pos.z + cs.tmpOffset.z + cs.size.z) + cs.gfxOffset.y`
  on the screen.
- `cs.size` affects the size of the sprite drawn into the screen.
- `cs.wallY` affects the drawing of the ground and wall sprites as follows:
  - for walls: cut `cs.size.y - cs.wallY` from the top of the source
  - for grounds: only draw `cs.size.y - cs.wallY` from the top of the source.
  If wallY results in a zero-size sprite (i.e. if wallY >= size.y), then
  nothing is cut.
- `cs.mergeTop`, if true, draws the ground part anyway.

- `cs.gfxCut` crops the border of the sprite. It is an object with attribute
  `left`, `right`, `top` and `bottom` indicating how much pixels to crop.

- `cs.flip.x` will flip the image vertically. Might be ignored in some cases.
- `cs.flip.y` will flip the image horizontally. Might be ignored in some cases.

- `cs.rotate` indicates how much to rotate the sprite, clockwise.
  (when reasoning with (x,y) coordinates, this is a positive angle, but since
   y points down, the result is a clockwise rotation)
- `cs.scale.x` and `cs.scale.y` indicates how much to scale the sprite
  horizontally and vertically. Negatives values are allowed and -1 is often
  used.

- `cs.pivot.x` and `cs.pivot.y` indicates the pivot used for rotations and
  scaling.
- `cs.alpha` affect the alpha blending of the entire sprite render operation.
  1 = fully opaque, 0 = fully transparent.
  Note that if `ig.system.context.globalAlpha` was not 1, then `cs.alpha` is
  multiplied by it.

The transformations are applied in this order :

1. If `flip.x` is true, it is applied first.
2. All cropping operations, either done by `gfxCut`, by removing wall or ground
   parts or by clipping between `zMin` and `zMax`, are done in parallel, and
   the one clipping the most is retained.
3. If `flip.y` is true, it is applied here.
4. scaling is applied
5. rotation is applied


The sprite is drawn as follow:

- Draw the sprite.
  How it is done actually depends on the type of the image contained in the
  sprite.  See Image Types below.
- If the sprite has a `cs.overlay.color`, then recolor the sprite with
  an uniform color and draw the result with alpha blending set to
  `cs.overlay.alpha` (relative to `cs.alpha`).
- If the sprite has a `cs.lighterOverlay.color`, then recolor the sprite by
  adding the color components instead of replacing it, then draw the result
  with alpha blending set to `cs.lighterOverlay.alpha` (relative to `cs.alpha`)

## Sprite Image Types

Entities uses various types of images in their sprites.

### ig.Image

This is the simplest type of image, directly loaded from a PNG file.
The source coordinates are used to select which part of the image is drawn.

Entities typically uses them using an Animation Sheet.

### ig.ImageCanvasWrapper

This image type behave like `ig.Image` but contains a canvas dynamically
constructed by the entities.

The most common user of `ig.ImageCanvasWrapper` are the various
`ObjectLayerView`-like entities (`ObjectLayerView`, `TeleportStairs`,
`OLPlatform` ("Object Layer Platform") and `BossPlatform`).  They work
by pre-rendering the Object maps into chunks, then wrapping each chunk into
a `ig.ImageCanvasWrapper`.  Then, the entities uses these chunks as sprites
to draw parts of the Object maps into the screen.

These entities are typically used to create maps more dynamic, by allowing
tiles to be moved, removed or made transparent.  They can also be used to
represent complex shapes with y-indexes that cannot be represented as maps.

Another user of `ig.ImageCanvasWrapper` are lights, but they are not drawn
as sprites.

### ig.ImagePattern

These are patches of images that are to be repeated, like textures.  The
texture is taken from an `ig.Image` stored in the `sourceImage` field.

The coordinates of the texture inside the source image are contained directly
inside `ig.ImagePattern`, using parameters passed to its constructor. They
are stored inside the `sourceX`, `sourceY`, `width` and `height` fields.

This object is typically mass-generated by `ig.ImagePatternSheet` or generated
with static parameters by individual entities types.

The constructor if `ig.ImagePattern` also take an `optMode` parameter, which
is used as an optimization hint. The optimization is to allocate an offscreen
canvas and pre-draw the texture several times on it, so that when it is time to
render, the number of `RenderingContext2D.drawImage` calls can be reduced.

It can take these values:

- `ig.ImagePattern.OPT.NONE`: Do not optimize.
- `ig.ImagePattern.OPT.REPEAT_X`: Pre-draw an horizontal stripe on a canvas
  with a minimum width of 256.
- `ig.ImagePattern.OPT.REPEAT_Y`: Pre-draw a vertical stripe on a canvas with
  a minimum height of 256.
- `ig.ImagePattern.OPT.REPEAT_X_OR_Y`: Pre-draw both a horizontal stripe and
  a vertical stripe.
- `ig.ImagePattern.OPT.REPEAT_X_AND_Y`: Pre-draw a square of minimum size
  256x256 with the texture.

When drawn, this image type uses the source image coordinate given by
`ig.Renderer2d.SpriteDrawSlot.draw()` only to shift the starting position of
the texture.  It is thus possible to create a scrolling texture by incrementing
the source coordinates indefinitely.  This effect is used by e.g. laser bridges.

### ig.SimpleColor

This image type represents a solid color, which uses a `fillRect` operation
to be drawn.  It is actually unused by the game.

### ig.SimpleCircle

This image type draws a filled circle with a colored border.  It is actually
unused by the game.

### ig.ComplexLineCircleBox

This image type draws a filled circle with a line pointing to a predetermined
target.  It is actually unused by the game.

### ig.TransitionColor

This image type is similar to `ig.SimpleColor`, but the solid color can vary
between a color and another color using an alpha parameter that can be adjusted
at runtime.

The game uses it only once, in the cargo ship hold, to make the teleporter glow.

### ig.DoubleColor

This image type contains two `ig.SimpleColor` or `ig.TransitionColor`, and
uses one color for the ground part and another color for the wall part.

They are only used by puzzle walls (entities `WallVertical` and
`WallHorizontal`).
