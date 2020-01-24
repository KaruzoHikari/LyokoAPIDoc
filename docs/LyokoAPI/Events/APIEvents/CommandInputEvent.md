# Command Input Event
This event is called whenever a command is executed in the game.
The commands can be prefixed by "api.", but LAPI automatically removes it before passing it to the plugins.
**Only application devs should call this event, DO NOT call this from your plugin.**

## Calling
This event takes a String, being the complete command (either with or without the "api." prefix).

```csharp
string myCommand = "api.plugins.list";
CommandInputEvent.Call(myCommand);
```

## CommandListener
It's highly recommend for plugin developers to use the [CommandListener](LyokoAPI/Commands/CommandListener.md) in order to work with commands.

## Subscribing
This event supplies a string, being the complete command **without the "api." prefix.**

```csharp
public class DIYListener
{
    public void StartListening()
    {
        CommandInputEvent.Subscribe(OnCommand);
    }

    public void OnCommand(string command)
    {
        //Do something with command
    }
}
```

