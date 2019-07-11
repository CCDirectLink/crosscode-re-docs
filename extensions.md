# Location

`assets/extension/*/*.json`

An extension is considered valid for loading if both:

A. There is a directory with the extension's name in the extension folder.

B. Within this directory, there is a file with the name `<extname>.json`, with `<extname>` being the actual extension name.

# Format

```
{
 "name": <LangLabel>,
 "description": <LangLabel>,
 "files": <Array, optional>,
 "entries": <Array of ExtensionEntry, optional>
}
```

# Summary Example

```
{
 "name": {"en_US": "The Fast Mouse", "langUid": 13371337},
 "description": {"en_US": "A fast mouse.", "langUid": 13371337},
 "files": ["data/enemies/mouse-bot.json"],
 "entries": []
}
```

# Files

The "files" table contains file overrides.

Any of the following:

+ JsonLoadable (`data/database.json` or similar, except `data/maps/`)
+ Level JSON (`data/maps/` such as `data/maps/henne-test-1.json`)
+ Sounds (`media/bgm/ability-got.ogg` etc.)
+ Images (`media/gui/basic.png` etc.)
+ and likely, in future, anything that somehow doesn't class as one of the above

...passes the asset path to 'getFilePath', which checks with the 'fileForwarding' object.

If it doesn't find anything, it returns the original path.

(ERRATA: A previous version of this document used made-up names which were incorrect here.)

Elements in the 'files' array are CrossCode file paths that are added to the 'fileForwarding' object.

An example for a map would be `data/maps/kdc-test-1.json`; note the lack of `assets/`.

As for an enemy, in the example `data/enemies/mouse-bot.json` is overridden.

It's standard for this documentation for paths to be referred to including the `assets/` prefix, but Extensions files do not have that.

# Entries

The "entries" array contains objects to be picked up by Extension listeners, registered with `ig.extensions.addListener`.

These elements have their own sub-format; they are objects of the form:

```
{
 "type": <Some type here, see below table. String>,
 "data": <Some data here, see below table. Usually object>
}
```

The 'type' property contains a string. Recognized types are:

## "skin"

Here, the 'data' field follows the same format the in-built 'holiday-hat' object does:

```
{
 "item": <Item ID number, such as 168 for the Holiday Hat. Controls the skin>,
 "autoAdd": <Boolean. If set to true, you are given the item automatically>,
 "type": <Meant to control which kind of skin change is applied. See the "playerskins" documentation for more details>,
 "settings": <Object specific to the skin change type. See the "playerskins" documentation for more details>
}
```

Note that right now, due to an inability to extend the Database from Extensions, you can only replace existing items with the same skin type.

In particular, the item must be defined, in the toggle set for the target skin type, and must have a PlayerSkins registration.

As an example of this, the "Kunoichi" item exclusive to ninja-skin users exists (but is unobtainable) in the game regardless of if the DLC is installed, and is togglable, but the Skin itself is not registered so it's useless.

# Examples

For examples of valid Extensions, see the "playerskins" folder in this repository, which should contain at least a Pet example at time of writing.

# Speculation

It is likely reasonably safe to assume that future versions of Extension will allow adding database entries.

Alternatively, there may already be ways to modify the database without copying the existing one in the current system.

