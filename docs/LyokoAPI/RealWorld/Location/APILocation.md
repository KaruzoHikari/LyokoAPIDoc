# APILocation
APILocation is an implementation of [ILocation](Abstract/ILocation.md). It represents any location that only requires a ``Name`` property.

# Instantiating
You can instantiate an APILocation like this:
```csharp
//EXAMPLE! DONT DO THIS AS A PLUGIN DEVELOPER.
LW_ArriveEvent.Call(LyokoWarriors.ODD, new APILocation("The NorthPole"));
```
# Properties
## Name
Returns a ``string``, being the name of the location.

# Methods
## [GetLocationName()](Abstract/ILocation.md#GetLocationName())
Returns [Name](##Name).

## [GetInnerLocation()](Abstract/ILocation.md#GetInnerLocation())
Returns an instance of itself. (An APILocation doesn't have inner locations).

## [AsGenericLocation()](Abstract/ILocation.md#AsGenericLocation())