# Location 

`assets/data/characters/*/*.json`


# When is it seen in game?

Faces are usually seen during cutscenes. They are the character expressions that are accompanied by the text.

# Format

```
{
    "face" : {
        "subImages" : {
            "nameOfSubImage" : "path/to/nameOfSubImage.png"
        },
        "width" : int,
        "height" : int,
        "centerX" : int,
        "centerY" : int,
        "src" : "path/to/src.png",
        "parts" : [{
            "nameOfPart" : {
                "srcX" : int,
                "srcY" : int,
                "width" : int,
                "height" : int,
                "destX" : int,
                "destY" : int,
                "subX" : int,
                "subY" : int,
                "img" : "nameOfSubImage"
            }
        }],
        "expressions" : [{
            anim : [int],
            time : float,
            repeat: int,
            faces : [
                [str]
            ]            
        }]
    }
}
```


# Explanation
| **Key** | **Info** |
|-----|------|
| `face` | stores the information about all the character expressions |
| `face.width` | How wide the reference image is |
| `face.height` | How tall the reference image is |
| `face.centerX` | idk |
| `face.centerY` | idk |
| `face.src` | default source image to use |
| `face.subImages` | special images to use |
| `face.parts` | the puzzle pieces for an expression |
| **Optional parts** |
| `face.parts[n].nameOfPart`| a thing that contains more things. |
| `face.expressions` | all expressions for the character |
