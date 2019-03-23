
# Location 

`assets/data/characters/*/*.json`


# When is it seen in game?

Faces are usually seen during cutscenes. They are the character expressions that are accompanied by the text.

# Format

```
{
    "face" : {
        "subImages" : {},
        "width" : int,
        "height" : int,
        "centerX" : int,
        "centerY" : int,
        "src" : "src.png",
        "parts" : [],  
        "expressions" : []
    }
}
```


# Face 
| **Key** | **type** | **Info** |
|-----| ----- | ------|
| `subImages` | [SubImage](#subimage) | ??? |
| `width` | [int](#integer) | How wide the reference image is |
| `height` | [int](#integer)| How tall the reference image is |
| `centerX` | [int](#integer) | idk |
| `centerY` | [int](#integer) | idk |
| `src`     | [Image Path](#img-loc) | default source image to use |
| `parts`   | [parts](#parts) | ??? | 
| `expression` | [expression](#expression) | ??? |


# Types

## <a id="integer">Integer</a>

A number 

---
---
---

## <a id="string">String</a>

A series of characters 

---
---
---
## <a id="subimage">SubImage</a>
```js
{
    "name" : "value"
}
```
| **key** | **type** | **info** |
| ------- | -------- | -------- |
|  `name`   |  [str](#string)     |  The name of the subImage (must be unique) |
|  `value`  |  [Image Path](#img-loc)     | ??? | 


---

## <a id="img-loc">Image Location</a>

`assets/media/face/*/*.png`

---
---
---
## <a id="parts">parts</a>

```js
{
    "parts" : [Part]
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
| `Part`  | [Part](#part)     | Array of body parts |

---

## <a id="part">Part</a>
```js
{
    "name" : PartConfig
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
| `name`  | [str](#string) | Body part name (unique) |
| `PartConfig` | [PartConfig](#part-config) | ??? |

---


## <a id="part-config">PartConfig</a>

```js
{
    "destX" : int,
    "destY" : int,
    "subX"  : int,
    "subY"  : int,
    "width" : int,
    "height": int,
    "srcX"  : int,
    "srcY"  : int,
    "img"   : str    
}
```

| **key** | **type** | **info** |
| ------- | -------- | -------- |
|  `destX` | [int]() | In game destination X-coord |
|  `destY` | [int]() | In game destination Y-coord |
|  `width` | [int]() | Width of body part in the image file|
|  `height`| [int]() | Height of body part in the image file  |
|  `srcX`  | [int]() | X-coordinate location in image file |
|  `srcY`  | [int]() | Y-coordinate location in image file |

**OPTIONAL** 

| **key** | **type** | **info** |
| ------- | -------- | -------- | 
| `subX`  | [int]()  | destX adjustment value |
| `subY`  | [int]()  | destY adjustment value|
| `img`   | [str]()  | SubImage to use (key name) |

 ---
---
---
## <a id="expression">expression</a>
```
[{
    anim : [int],
    time : float,
    repeat: int,
    faces : [Face]         
}]
```

| key    | type  | info |
|--------|-------|------|
| anim   | Array#int | Each index is a face frame to play  |
| time   | float | Time between each new frame |
| repeat | int   | How many times to repeat |
|        |       | value (n) behavior  |
|        |       | n > 0 - How many times to play again|
|        |       | n == 0 - Only play once|
|        |       | n < 0 - Play forever|
| faces  | [Array#Face](#face)  | ??? |

 ---

 ## <a id="face">Face</a>
 ```
[
    str,
    ...
    str
]
```
| key    | type  | info |
|--------|-------|------|
| index  | int   | Not an explict key. Corresponds to which part it's from. |
| value  | str   | Name of part.|
 ---


# EXTRAS

The faces reference point is at 192px on the y-axis.

The x-axis is more variable and depends on which side its on.

LEFT is 32px.

RIGHT is 408px.

*Note: Assumes dimensions are 568px, 320px.
 