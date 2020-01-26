# ITower
An interface representing a Tower on a VirtualWorld
It also implements [ILocation](../../RealWorld/Location/Abstract/ILocation.md)

# Properties
  + Number - the number of the ITower.
  + Activated - whether or not the ITower is activated. Preferably this is `!= APIActivator.NONE`<br>  
  + Sector - the [ISector](./ISector.md) this ITower is a member of.<br>
  + Activator - the current [APIActivator](../../VirtualStructures/APIActivator.md) that this tower is under control of.

##Notes
ITower does not have a public setter on Activator, so if it is used through the interface,
like so:
```csharp
ITower tower = new APITower("lyoko","ice","1");
```
You can't change its Activator directly.<br>  
You can access the full location of the ITower by getting the ISector and its IVirtualWorld.<br>  
*Hint: If the implementation is APITower, it's not guaranteed that the Sector and the VirtualWorld have other data besides the tower.
See [APITower](../../VirtualStructures/APITower.md) for more information.*
