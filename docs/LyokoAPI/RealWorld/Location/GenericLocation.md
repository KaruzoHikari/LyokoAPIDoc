# Generic Location
Generic Location is a class that unifies the different types of [ILocation](Abstract/ILocation.md). For example, both [APILocation](APILocation.md) and Sector are ILocations, but they work very differently. 

# Knowing the location type
There are several methods you can use to find the real location type being the GenericLocation

## GetLoccationType
This method will tell you the [LocationType](Abstract/LocationType.md). It will return ``API`` if the Type is not ``SECTOR`` or ``TOWER``.

## IsSector()
Returns wether or not the location is a [ISector](../../VirtualStructures/Interfaces/ISector.md)

## IsTower()
Returns wether or not the loation is a [ITower](../../VirtualStructures/Interfaces/.md)

## IsAPILocation
Returns wether or not the location is an APILocation

# Getting the actual location
Once you know what type the location is, you can get the actual location type.

## Name
You can get the ``string`` name of a location with:
```csharp
LyokoWarriors.ODD.Location.GetLocationName();
```

## Dynamic
You can get a ``dynamic`` location like this:
```csharp
dynamic oddslocation = LyokoWarriors.ODD.Location.GetDynamicInnerLocation();
oddslocation.GetLocationName(); //we don't know if this Location has this method available, so BE SURE.
```
A ``dynamic`` type is a special type where you can call any method, but it will throw an exception if the method doesn't exist.
**BE SURE TO VERIFY WHICH LOCATION TYPE YOU ARE GETTING**

## ITower
If the location is a tower, you can get it like this:
```csharp
ITower tower;
if(LyokoWarriors.ODD.Location.TryGetInnerTower(out tower)) //checks if the location is actually a tower
{
    //do something with this location.
}else
{
    //something went wrong
}
```

## ISector
If the location is an ISector, you can get it in the same way as above, with the ``TryGetInnerSector()`` method.

## APILocation
[APILocation](APILocation.md) doesn't have any extra methods, so you don't need to get it as a Type. You can always get the ``string`` name with [GetLocationName()](##Name).
