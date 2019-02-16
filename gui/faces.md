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
|  `destX` | [int]() | ??? |
|  `destY` | [int]() | ??? |
|  `width` | [int]() | ??? |
|  `height`| [int]() | ??? |
|  `srcX`  | [int]() | ??? |
|  `srcY`  | [int]() | ??? |

**OPTIONAL** 
| **key** | **type** | **info** |
| ------- | -------- | -------- | 
| `subX`  | [int]()  | ??? |
| `subY`  | [int]()  | ??? |
| `img`   | [str]()  | ??? |

 ---
---
---
## <a id="expression">expression</a>
```
[{
    anim : [int],
    time : float,
    repeat: int,
    faces : [
        [str]
    ]         
}]
```