# PropInteract
`sc.PropInteract`


## STRUCTURE

```ts
declare class PropInteract {

    // settups up the incoming prop's interact
    init(prop, settings: PropInteractSettings)

    // adds interact entry
    // returns true if prop has permaEffect set
    onShow() : boolean

    // setups up the supplied permaEffect on the Prop
    onPermaUpdate()

    // pretty much the destructor
    onKill()

    // triggers if the interact has an event, otherwise returns false
    // never returns true
    onInteraction() : boolean
};

```


## SETTINGS

```ts
declare type PropInteractSettings = {
    "icon": PropInteractIcon, // default: "INFO"
    
    // optional fields
    "event": Event[],

    "permaEffect": Effect,

    // if true, can interact during combat
    "combatOkay": boolean, // default: false

    // only works if event is set
    "cutsceneType": EventType // default: "CUTSCENE"

};
```

Should only focus on PropInteractSettings if you are spawning an entity that needs it.