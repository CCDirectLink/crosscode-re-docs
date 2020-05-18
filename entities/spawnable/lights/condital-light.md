# Conditional Light
`ig.ENTITY.ConditionalLight`

# Structure
inherits from [Entity](/entities/base/entity.md)

```ts
declare type ConditionalLight = {
    "type": "ConditionalLight",
    "settings": {
        "condition": VarCondition,

        // how big the shine of the light will be
        "lightSize": LightSize,

        "glowSize": LightSize,

        // if the weather type has a glowColor property,
        // then it is used 
        "weather": WeatherTypes,

        // weather field is ignored if this is set
        // string is a hex color. Format of "#xxxxxx" where x is a hex digit 
        "glowColor": string,

    }
};
```

### External Type References

[VarCondition](/types/var-condition.md)

[LightSize](/types/light-size.md)

[WeatherTypes](/types/weather-types.md)