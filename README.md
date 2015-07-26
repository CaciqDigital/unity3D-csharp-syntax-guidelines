# C# Unity Syntax Guide

## Layout
### Indentation
Tab = 4 spaces - let the IDE convert for you. (It is easy to get the indentation size you like i.e. 4 spaces. The inverse transformation, from 4 spaces to TAB is difficult.)

```c#
public int whoop () {
    // ...
}
```

### Braces
Braces should be on the same line preceded by a space - K&R style

```c#
public int whoop () {
    // ...
}
```
if/for loops should always have an accompanying opening and closing brace

```c#
if (troop.Name == "Vader") {
    // ...
}

for (var i = 0; i < troops.length; i++) {
    // ...
}
```

### Spaces
Quick Summary

Good
```c#
for (var i = 0; i < length; i++) {
    // whooperize
}

var playerName = (String.IsNullOrEmpty(player.Name)) ? "Friend" : player.Name;
```

Bad

```c#
for(var i=0;i<length;i++) {
    // whooperize
}

var playerName=(String.IsNullOrEmpty(player.Name))?"Friend":player.Name;
```

**1. Before parentheses**

Good
```c#
Public int CalculateDistance () {

}
```

Bad
```c#
Public int CalculateDistance(){

}
```

**2. After comma in parentheses**

Good

```c#
Public int CalculateDistance (Agent player, Agent enemy) {

}
```

Bad

```c#
Public int CalculateDistance (Agent player,Agent enemy) {

}
```

**3. After comma in multiple field declarations**

Good

```c#
Troop vader, maul, palpatine;
```

Bad

```c#
Troop vader,maul,palpatine;
```

**4. Around operators**

Good

```c#
if (x > y) {

}
```

Bad

```c#
if (x>y) {

}
```

### Blank Lines

**1. After using declarations**

Good

```c#
using UnityEngine;
using UnityEngine.UI;

public class PlayerManager : MonoBehaviour {
 
```

Bad

```c#
using UnityEngine;
using UnityEngine.UI;
public class PlayerManager : MonoBehaviour {
 
```

**2. Between Member declarations**

Good

```c#
public class PlayerManager : MonoBehaviour {

    public static void Simulate () {
        //...
    }

    public static void Visualize () {
        //...
    }  
```

Bad

```c#
public class PlayerManager : MonoBehaviour {
    public static void Simulate () {
        //...
    }
    public static void Visualize () {
        //...
    }  
```



## Casing
Class: Pascal	
```c#
AppDomain
```

Enums: Pascal
```c#
ErrorLevel
```

Event: Pascal	
```c#
ValueChange
```

Exception: Pascal
```c#
WebException // Always ends with the suffix Exception.
```

Read-only Static field: Pascal
```c#
RedValue
```

Interface: Pascal
```c#
IDisposable // Always begins with the prefix I.
```

Method: Pascal
```c#
ToString
```

Namespace: Pascal
```c#
System.Drawing
```

Parameter: Camel
```c#
typeName
```

Property: Pascal
```c#
BackColor
```

Protected instance field: Camel // rather use a property if you can
```c#
redValue
```

Public instance field: Pascal // rather use a property if you can
```c#
RedValue
```

## Implicitly Typed Local Variables

Use var when the the type of a variable is clear from the context.

```c#
// we can easily see what the follow types will be
var troops = new List<Troop>{stormtrooper, atatDriver, atstPilot};
var playerName = player.Name;
var messages = new StringBuilder(1000);
var weapons = new Dictionary<String, Weapon>();
```

Much easier to read than:
```c#
IList<Troop> troops = new List<Troop>{stormtrooper, atatDriver, atstPilot};
String playerName = player.Name;
StringBuilder messages = new StringBuilder(1000);
Dictionary<String, Weapon> weapons = new Dictionary<String, Weapon>();
```

## Class Naming Guidelines
1. Use a noun or noun phrase to name a class.
```c#
Employee
```
2. Use Pascal case.
```c#
Employee
```
**Other Notes**

Use abbreviations sparingly.

Do not use a type prefix, such as C for class, on a class name. For example, use the class name FileStream rather than CFileStream.

Do not use the underscore character (_).

Occasionally, it is necessary to provide a class name that begins with the letter I, even though the class is not an interface. This is appropriate as long as I is the first letter of an entire word that is a part of the class name. For example, the class name IdentityStore is appropriate.

Where appropriate, use a compound word to name a derived class. The second part of the derived class's name should be the name of the base class. For example, ApplicationException is an appropriate name for a class derived from a class named Exception, because ApplicationException is a kind of Exception. Use reasonable judgment in applying this rule. For example, Button is an appropriate name for a class derived from Control. Although a button is a kind of control, making Control a part of the class name would lengthen the name unnecessarily.

## Commenting

1. Single space before the start of the comment

Good 

```c#
// this is a comment
// TODO: make this configurable
```

Bad

```c#
//this is a comment
//TODO: make this configurable
```