# LAPIListener
The LAPIListener class is a helper class to easily work with events and to prevent unnecessary boilerplate code.<br>

To make a LAPIListener, just extend your listener class like so:
```csharp
public class MyExampleListener : LAPIListener
```
<br>

# Listening to events
To listen to events, you first need to enable the listener.
In your main plugin class, or wherever you need the listener to be, write this:

```csharp
LAPIListener listener = new LAPIListener();
listener.StartListening();
```

Similarly, you can stop listening to events **(which you may have to according to the [Rules](LyokoPlugin/introduction.md))**: 
```csharp
listener.StopListening();
```

To listen to a specific event, override it's method:
```csharp
public class MyExampleListener : LAPIListener
{
  public override void onLW_Death(LyokoWarrior warrior)
  {
    //Some code that runs when a LW dies
  }
}
```
The details about each event can be found in the rest of the documentation.

You can find a list of events that the LAPIListener currently supports by checking out the class itself on GitHub. For the master branch, this is: https://github.com/LyokoAPI/LyokoAPI/blob/master/LyokoAPI/API/LAPIListener.cs


# DIY Listener
You can also choose not to use a LAPIListener, although it is not recommended. 

### Subscribing
The point of an event is that code is executed when the event is called.
A method that waits for an event to happen, is usually called a Listener.
We will call adding a listener "**Subscribing**".

A method that subscribes to an event must be of a certain format.
For example, a TowerEvent requires a Tower parameter.
The format of a method is called a **delegate** in C#.
*Hint: You can find all the delegates on the pages that describe the events.*

You can subscribe to an event with: ``SomeEvent.Subscribe(method)``

In practice, you can use a method or a lambda.
For example:
```csharp
public Listener()
{
  TowerActivationEvent.Subscribe(onTowerActivation);
}

public void onTowerActivation(ITower tower)
{
  Console.WriteLine("Tower {0} {1} activated!",tower.Sector.Name, Tower.Number);
}
```
Can also be written as:
```csharp
public Listener(){
  TowerActivationEvent.Subscribe(tower =>
  Console.WriteLine("Tower {0} {1}",tower.Sector.Name,tower.Number));
}

```
### Unsubcribing
As a dev, you might want to stop listening to an event.
For example, it's good practice to stop listening if your plugin is disabled.

To unsubscribe from an event, you need to have it stored in a variable.
The easiest way to do this is:
```csharp
var listener;
public void StartListening()
{
  listener = SomeEvent.Subscribe(foo => foo.Bar());
}

public void StopListening()
{
  SomeEvent.Unsubcribe(listener);
}

```