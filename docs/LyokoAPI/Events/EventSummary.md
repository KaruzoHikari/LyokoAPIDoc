# Events
The core of LAPI's workings is the usage of events.
These are messages that are typically sent by the Application, and processed by a Plugin.
Here's an oversight of how they work.

## Attention!
The documentation below is provided mostly for more advanced understanding of LAPI or special use cases. For simple handling of events, check out the documentation for [LAPIListener](LAPIListener.md)

## Listening
In order to write interesting plugins, we want to make things happen when certain things ("events") happen in the game.

More concrete, we are going to make code run when an event is "called". We call this "Listening" or "Subscribing" to an event.

The easiest way to listen to events is using a [LAPIListener](LAPIListener.md). You will find more in-depth explanation there.


## Calling
As an Application Developer, you'll want to notify your plugins (or other parts of your application) of certain events.
LAPI is designed to make this simple.
Do remember that if you pass an object, like a Tower to an event, listening methods will be able to change that object. 
(Unless you set variables to be internal, which you should do anyways).

This is why we recommend you use LAPI's built-in classes to create objects based on your code.
(see [ITower](./Interfaces/ITower) and [APITower](./VirtualStructures/APITower) for more info)
That is, unless you want your Application's data accessible.

Calling an event is simple: ``SomeEvent.Call(/*parameters*/)``

For example, you could do:
```csharp
TowerDeactivationEvent.Call(new APITower("lyoko","ice",1));
```
You can find more examples on the specific event pages.
