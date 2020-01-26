# APITower
This class is an implementation of [ITower](./Interfaces/ITower.md)

# Properties
Identical to [ITower](./Interfaces/ITower.md)
with the following differences:
  + Activator has a public setter
  + Activated returns true if the Activator isn't NONE

# Constructors
This class has two constructors:
```csharp
APITower(int number, ISector sector);
```
This implies that the APITower belongs to an existing [ISector](./Interfaces/ISector.md).

```csharp
APITower(string vworld, string sector, int number);
```
This not only creates a new APITower, **but it also creates a new ISector with a new IVirtualWorld.**<br>
This means that the towers' VirtualWorld contains one sector, and that sector contains this tower.

##Equals()
This class has it's own Equals method.<br>
However, it does not change the hash, so in a Hashmap or something similar, it will not follow the rules of Equals().<br>

An object is equal to 'this' APITower if these conditions are all true:<br>
  <ul>
    <li>It's an ITower</li>
    <li>It's ISector has the same name</li>
    <li>It's IVirtualWorld has the same name</li>
  <ul>

# Methods
## [GetLocationName()](../RealWorld/Location/Abstract/ILocation.md#GetLocationName())
For the tower ``Lyoko Ice 1``: ``"Lyoko : Ice,Tower 1"``
## [GetInnerLocation](../RealWorld/Location/Abstract/ILocation.md#GetInnerLocation())
Returns itself.