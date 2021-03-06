#Tower Activation Event

##Subscribing
This event expects a ``void Method(ITower tower)``<br>
Since it uses an ITower, it's fairly read-only.

##Calling
This events has a few parameters you can supply in Call().<br>
There are important differences between them, so read carefully.<br>
*Note: It will not be called if the supplied tower isn't activated.*

###Call with [ITower](../../VirtualStructures/Interfaces/ITower)
*Note: We don't generally recommend this.*<br>
You can call the event by supplying an implementation of ITower.<br>
This assumes that the Activator is already set.<br>
We only recommend this if you've chosen to base your Application's Tower class to implement ITower.

###Call with [APITower](../../VirtualStructures/APITower), [APIActivator](../../VirtualStructures/APIActivator)

*Hint: The benefit of this method is that you're not giving direct access to your own Tower class, if thats what you want.*  

You can call the event by supplying an APITower and an APIActivator.<br>
There are many ways to do this, but you'll likely use the following:<br>
```csharp
TowerActivationEvent.Call(new APITower("Lyoko","ice",1),APIActivator.XANA)
```
Or, if you want to do it 'the hard way', you could also do:
```csharp
APITower tower = new APITower("Lyoko,ice,1")
TowerActivationEvent.Call(tower,APIActivator.XANA);
```
But in that case, you might as well use ITower as an argument.

This approach is almost identical to:
###Call with Strings
You can also call the event with only strings.
Just like before, you won't be giving any access to your own tower class this way.

```csharp
TowerActivationEvent.Call("lyoko","ice",1,"XANA");
```

This __will__ throw an exception if the activator is invalid, so make sure to get it right, or to put it in a try/catch.
