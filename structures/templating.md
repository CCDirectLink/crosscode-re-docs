# Location

Any JsonLoadable and a few not-JsonLoadables.

# Data Format

At the root of the object, the "jsonTEMPLATES" property may be present.

This contains a sub-object - keys are the names of templates, values are templates as described in "Template Format".

Other templates are defined by the game itself.

A template may be instanced using the property "jsonINSTANCE" in any part of the object.

This property causes a template to be instanced *in place of* the object.

Other properties in that object are then parameters for the template.

# Template Format

# Example

```
{
 "jsonTEMPLATES": {
  "32TS": {"src": {"jsonPARAM": "src"}, "width": 32, "height": 32}
 },
 "namedSheets": {
  "a": {"jsonINSTANCE": "32TS", "src": "very-interesting.png"},
  "b": {"jsonINSTANCE": "32TS", "src": "bunch-of.png"},
  "c": {"jsonINSTANCE": "32TS", "src": "copy-pasted-sheets.png"}
 }
}
```
