# CommandException
CommandException is a class that extends [LapiException](Exceptions/LapiException.cs).

It's an exception designed for use with [Command](Command.md).

# Constructor
To instantiate a CommandException, you need to supply an ICommand and a message.

```csharp
public class MyCommand
{
    //see Command.md for the full code
    public override void DoCommand()
    {
        throw new CommandException(this, "A big big error!");
    }
}
```

# Resolve()
The [Resolve](LyokoAPI/Internal/LAPIException.md#Resolve()) method for this LAPIException sends a CommandOutputEvent with the given message.