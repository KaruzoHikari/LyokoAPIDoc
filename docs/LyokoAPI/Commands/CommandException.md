# CommandException
CommandException is a class that extends [LapiException](Exceptions/LapiException.cs).

It's an exception designed for use with [Command](Command.md).

# Constructor
To instantiate a CommandException, you need to supply a ICommand and a message.

```csharp
public class MyCommand
{
    //see Command.md for the full code
    public override void DoCommand()
    {
        throw new CommandException(this, "a big big errror!");
    }
}
```

# Resolve()
The [Resolve](LyokoAPI/Internal/LAPIException.md#Resolve()) method for this LapiException sends a CommandOuputEvent with the given message.