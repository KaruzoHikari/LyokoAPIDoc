# Command Output Event
This event is called whenever a command wants to send feedback to the user.

## Command class
The [Command class](LyokoAPI/Commands/Command.md) has a built-in method to call this event.

## Calling
This event takes two Strings: the name of the command, and the message.

```csharp
string message = "Music paused.";
CommandOutputEvent.Call("LyokoDJ",message);
```
The game will display it like this: ``[LyokoDJ] Music paused.``

## Listening
This event supplies a string, being the complete output including the name of the sending command.

**Only application devs should listen to this event.**

```csharp
public class DIYListener
{
    public void StartListening()
    {
        CommandOutputEvent.Subscribe(OnCommand);
    }

    public void OnCommand(string command)
    {
        //Do something with CommandOutput, like showing it in-game
    }
}
```