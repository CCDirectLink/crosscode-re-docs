# EffectPreviewer
`ig.ENTITY.EffectPreviewer`

## Structure
inherits from  [Actor Entity](/entities/base/actor-entity.md)

## Example Usage

```js

// this is necessary for this entity to be useful in game
window.parent.EXTERNAL_IG_MESSAGE = function(msgName, value) {
    ig.game.onExternalMessageReceived(msgName, value);
}

// this is how you load new effect sheets
ig.game.sendExternalMessage("UPDATE_EFFECT_SHEET", "specials.shock");

// wait until loaded to do this
ig.game.sendExternalMessage("PLAY_EFFECT", {
   // the name
   "name": "",
   // this is the usual settings
   "settings" : {}
})

// stop the currently playing effect
ig.game.sendExternalMessage("STOP_EFFECT")

// update animation sheet of entity

ig.game.sendExternalMessage("EFFECT_PREVIEWER_APPEARANCE", {
    "size": {
        "x": 16,
        "y": 16,
        "z": 16
    },
    "animSheet": "player" // DotPath
});
```

### External Type References

[DotPath](/types/dot-path.md)

# Notes

The animation loaded defaults to player