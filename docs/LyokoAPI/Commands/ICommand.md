# ICommand
The ICommand interface is designed to allow a Plugin Dev or Application Dev to implement their own command class that can be used with the [CommandListener](CommandListener.md).

A default implementation is already available: [Command](Command.md).

# Members
### Name
The name is the full name of the command. this is used to call it in the [CommandListener](CommandListener.md).

This has to be the command that the user has to type.
For example the command ``api.dj.play`` has the Name ``play``

### DisplayName
The Display Name is the name that will displayed to the user, for example as command output.

This can be the same as Name, but it can be different in case the original command is too long.

For example the command ``api.dj.playthenextsong`` has the Name ``playthenextsong`` but could have the DisplayName ``playnext``.

This way, the output would be formatted as:
```
[playnext] Playing the next song!
```

# Methods
### Run()
The Run method takes a ``string[]``, being the arguments to the command.

This method is called by the [CommandListener](CommandListener.md).
The passed arguments are separated based on the ``.`` seperator.

For example the command ``dj.play.finalcountdown``, where the root command is ``dj`` has the arguments ``play`` and ``finalcountdown``.

