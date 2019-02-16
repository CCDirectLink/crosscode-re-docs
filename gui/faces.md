<style>
    a { 
        text-decoration: none; 
        color : "black"; 
    }
    a:hover { 
        text-decoration: none; 
        color : "black"; 
    }
</style>

# Location 

`assets/data/characters/*/*.json`


# When is it seen in game?

Faces are usually seen during cutscenes. They are the character expressions that are accompanied by the text.

# Format

```
{
    "face" : {
        "subImage" : {},
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
| `subImage` | [subImage](#subImage) | ??? |
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

## <a id="string">String</a>

A series of characters 

## <a id="subimage">subImage</a>
```js
{
    "name" : "value"
}
```
| **key** | **type** | **info** |
| ------- | -------- | -------- |
|  `name`   |  [str](#string)     |  The name of the subImage (must be unique) |
|  `value`  |  [Image Path](#img-loc)     | ??? | 


## <a id="img-loc">Image Location</a>

`assets/media/face/*/*.png`

## <a id="parts">parts</a>

```js
{
    "parts" : []
}
```




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