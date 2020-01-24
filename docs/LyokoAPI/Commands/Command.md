# Command
The Command class implements [ICommand](ICommand.md).
It tries to offer an easy-to-use template for Plugin Developers and Application Developers and is meant to work with the [CommandListener](CommandListener.md).

For each command you want to add to your plugin, you will have to extend this class.
```csharp
public class MyHelpCommand : Command
{
    //Code here
}
```

# Members
Command inherits the following members from [ICommand](ICommand.md):
* [Name](ICommand.md#Name)
* [DisplayName](ICommand.md#DisplayName) 

*(Note: DisplayName defaults to Name in this implementation)*

## MinArgs
This int defines the minimum amount of arguments that have to be passed. 
If there are less arguments than this number, the Command will throw a [CommandException](CommandException.md).

Defaults to ``0``

## MaxArgs
This int defines the maximum ammount of arguments that can be passed.
If there are more arguments than this number, the Command will throw a [CommandException](CommandException.md).

Defaults to ``Int32.MaxValue``

## SubCommands
A list of ICommands that are subcommands of this Command.
More info in the SubCommands section.

## Usage
This string shows the usage of a command. It's the "help message".\
By default it's a list of subcommands for this command.\
**If your command does not have subcommands, it's a good idea to set this value to something else.**

# Abstract methods
These methods have to be implemented when you extend this class.

## DoCommand()
This method is called when your command is executed. You will have to put your command-specific logic here.

It takes a ``string[]``, being the arguments to the command.\
It returns a boolean, being wether or not the command was successful (the return value is currently not used)

```csharp
protected override bool DoCommand(string[] args) //command api.talk.hello 
{
    if (args[0] == "hello")
    {
        Output("world"); //You can find more info about this method below
        return true; //Command succeeded
    }
    else if(args[0] == "world")
    {
        Output("hello");
        return true;
    }
    else
    {
        throw new CommandException(this, "Invalid argument!");
        //return false; //Not needed because of the exception
    }
}
```

# Useful Methods
These methods are helper methods for when you write your Command.

## Output()
You can use this method to send output to the user.
```csharp
Output("It'sa me, Mario!");
```
The output will be:
``[CommandName] It'sa me, Mario!``

## CheckLength()
This method is used to check the length of the arguments.\
This is automatically done before the command runs, based on MinArgs and MaxArgs. However, it may be useful to filter more down the line.\
It's not recommended to use this for subcommands, since there is already a system in place for those.

It takes a minimum value, and an optional maximum value.\
It will throw a [CommandException](CommandException.md) if the requirements are not met.

The Command class will automatically catch it and output a message to the user.

```csharp
protected override bool DoCommand(string[] args) //command.talk.hello.there
{
    if (args[0] == "hello")
    {
        CheckLength(2); //Minimum 2 arguments, or throw an exception
        if(args[1] == "there")
        {
            Output("GENERAL KENOBI!");
        }
        else
        {
            Output("Hi!");
        }
    }
    else
    {
        throw new CommandException(this, "invalid argument!")
        //return false; //Not needed because of the exception
    }
}
```

## CheckNumber()
This method can be used to check if an argument is a number.\
It takes the index of the argument (starting with 0), and it returns an int if the argument IS a number and throws a [CommandException](CommandException.md) if the argument is NOT a number.

```csharp
protected override bool DoCommand(string[] args) //command: api.add.1.2
{
    int number1 = CheckNumber(args[0]); //Should be '1'
    int number2 = CheckNumber(args[1); //Should be '2'
    Output($"{number1} + {number2} = {number1 + number2}");
}
```
# SubCommands
If you have a command that requires more than one argument, for example ``dj.play.finalcountdown``, it's best to use SubCommands.

## Adding subcommands
First, create a class that acts as a subcommand.
For example the command ``dj`` with the subcommand ``play``.

```csharp
public class PlayCommand : Command
{
    public override string Name {get;} = "play";
    public override string DisplayName {get;} = "dj.play"; //Optional, defaults to 'play' in this case.
    public override string MinArgs {get;} = 1;
    public override string MaxArgs {get;} = 1;
    public override string Usage {get;} = "Play a song by its name";

    public override void DoCommand(string[] args)
    {
        //code that plays the song
    }

}
```
Then, add this subcommand to the main command
```csharp
public class DjCommand : Command
{
    public override string Name {get;} = "dj";
    public override string MinArgs {get;} = 2;
    //No MaxArgs because we can't predict the MaxArgs of subcommands
    public virtual List<ICommand> subCommands {get; protected set;} = new List<ICommand>(){new PlayCommand()};
}
```
It's also possible to make a default constructor and add commands that way (the subcommand list is initialized by default)

Now we have to actually run subcommands when needed:
```csharp
public class DjCommand : Command
{
    //Name, args and subcommands like above
    protected override void DoCommand(string[] args)
    {
        if(args[0] == "help")
        {
            Output(Usage);
            return true;
        }
        DoSubCommand(args); 
    }
}
```
**Note: The DoSubCommand() method assumes two arguments were given, one being the subcommand, and one being the argument to the subcommand. It will simply ignore any command that doesn't have two arguments.**

The user will get a message if the subcommand does not exist.
