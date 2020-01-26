# Lyokowarriors
The LyokoWarriors class is a enum-ish class that provides the [Lyokowarrior](LyokoWarrior.md) object associated with a [LyokoWarriorName](LyokoWarriorName.md).



# Getting a LyokoWarrior
You can get a LyokoWarrior either by a string name, a static name, or it's [LyokoWarriorName](LyokowarriorName.md)

## By string name
If you have to work with a string, for example when you are using user input, you can get it like this:

```csharp
string name = "ODD";
Lyokowarrior warrior = LyokoWarriors.GetByName(name);
```
It will throw an ``ArgumentException`` if the warrior does not exist.

## By static name
You can get a specific LW like this:
```csharp
//check the HP of William
int hp = Lyokowarriors.WILLIAM.HP
```

## By LyokoWarriorName
You can also use [LyokoWarriorName](LyokoWarriorName.md) to find a Lyokowarrior:
```csharp
LyokoWarrior warrior = LyokoWarriors.GetByName(LyokoWarriorName.ODD)
```



