# Entity

This is the bare bone structure for any Entity types.

## Structure
> Note: You can not spawn an entity by itself

```js
declare type LevelObject = {
    "offset": Number,
    "level": Integer
};

declare type Level = Integer | LevelObject;

declare type Entity = {
    "x": Integer,
    "y": Integer,
    "level": Level
}
```