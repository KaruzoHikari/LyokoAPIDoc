# APIActivator
A person or entity that can activate an [ITower](./Interfaces/ITower.md)

# Values
XANA, JEREMIE, HOPPER<br>
NONE - the activator when the ITower is inactive.

# Parsing
If you want to parse a string to an Activator,<br>
you can use LyokoParser.

The methods below can also be applied to a specific activator, like ``APIActivator.XANA.Parse()``, although that's pretty silly to do.

## ParseActivator
Accepts a string, returns an APIActivator. <br>
Throws a FormatException if the string is invalid.
```csharp
APIActivator activator;
try{
  activator = LyokoParser.ParseActivator("XANA")
}catch (FormatException e) {
  LyokoLogger.Log(plugin.Name,e.Message); //will output something like 'Invalid activator: (activatorstring)!'
}
```

## TryParseActivator
Accepts a string, returns a boolean if it's a valid Activator.<br>
If true, stores it in a given variable.
```csharp
APIActivator activator;
if (!LyokoParser.TryParseActivator("XANA", out activator)) {
  LyokoLogger.Log(plugin.Name,"Not a valid activator!")
}
```
