# C# Unity Syntax Guide
## Summary
A starting point for a great C# syntax guide that can be easily shared between team members. Mono and Visual Studio/ReSharper project settings files available for import. 

## File Management
Use one class per source file. Avoid inner classes.

## Layout
### Indentation
Tab = 4 spaces - let the IDE convert for you. (It is easy to get the indentation size you like i.e. 4 spaces. The inverse transformation, from 4 spaces to TAB is difficult.)

```c#
public int whoop () {
    // ...
}
```

### Ordering
Elememts must be ordered by access, but lets keep Unity editor vars or implementations first in their relevant sections.

Within a class, struct, or interface, elements must be positioned in the following order:
* Constant Fields
* Fields
* Constructors
* Finalizers (Destructors)
* Delegates
* Events
* Enums
* Interfaces
* Properties
* Indexers
* Methods
* Structs
* Classes

Elements of the same type must be positioned in the following order by access level:
* public
* internal
* protected internal
* protected
* private

All static elements must be placed above all instance elements of the same type.

Example
```c#
public class WeaponManager : MonoBehaviour {
    #region fields
    // unity editor properties
    [SerializeField, Tooltip("A helpful tip")]
    int minSize = 0;
	
    [SerializeField, Tooltip("A helpful tip")]
    int maxSize = 10;
    
    // const first
    cost string someConst = "My Const";

     // public
    public int CurrentSize {get; set;}

    // private 
    int counter;
    int[] someInt;
    #endregion
    
    #region Methods
    public void Shoot () {
    }

    #region Unity interface implementations
    void Start () {
    
    }
    
    void Update () {
    
    }
    #endregion
    
    void calculateDistance () {
    }
    #endregion
}

public class Weapon : IWeapon {
    #region fields
    // const first
    cost string someConst = "My Const";
    
    // public
    public int CurrentSize {get; set;}

    // private 
    int counter;
    int[] someInt;
    #endregion
    
    #region Methods
    public override void Shoot () {
    }

    void calculateDistance () {
    }
    #endregion
}
```

### Exposure - NB
Expose the minimum needed from the class. Don't use public variables, use public properties with private setters instead.

Good

```c#
public class Watergun : IWeapon {
    public int RoundsRemaining {get; private set;}
    
    public void Fire () {
    	RoundsRemaining = RoundsRemaining--;
    }
}
```

Bad

```c#
public class Watergun : IWeapon {
    public int RoundsRemaining;
}
```

Good

```c#
public class WeaponManager : MonoBehaviour {
    [SerializeField, Tooltip("The current weapon")]
    Weapon currentWeapon;
    
    public CurrentWeapon {
    	get {
    	    return currentWeapon;
    	}
    }
    
    public void ChangeWeapon (Weapon newWeapon) {
    	currentWeapon = newWeapon;
    }
}
```

Bad

```c#
public class Watergun : MonoBehaviour {
    [SerializeField, Tooltip("The current weapon")]
    public Weapon currentWeapon;
}
```

### Properties VS Methods
In general, methods represent actions and properties represent data. Properties are meant to be used like fields, meaning that properties should not be computationally complex or produce side effects. When it does not violate the following guidelines, consider using a property, rather than a method.

### Braces
Braces should be on the same line preceded by a space - K&R style

```c#
public int whoop () {
    // ...
}
```
Conditional statements and loops should always have an accompanying opening and closing brace - irrespective of the number of lines required.

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
    #region Fields
    
    int count;
    
    string name;
    
    IList<Weapon> weapons;
    
    #endregion
}
```
Bad
```c#
public class PlayerManager : MonoBehaviour {
    #region Fields
    
    int count; 
    string name;
    IList<Weapon> weapons;
    
    #endregion
}
```

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

**2. Before return statements **
Good

```c#
public class PlayerManager : MonoBehaviour {
    #region Methods
    
    static Weapon AddWeapon (Weapon weapon) {
        weapon.Agent = this;
	weapon.Initialise();
	weapons.Add(weapon);
	
	return weapon;
    }

    public static void Visualize () {
        weapon.Agent = this;
	weapon.Initialise();
	weapons.Add(weapon);
	return weapon;
    }
    
    #endregion
```

Bad

```c#
public class PlayerManager : MonoBehaviour {
    #region Methods
    
    public static void Visualize () {
        weapon.Agent = this;
	weapon.Initialise();
	weapons.Add(weapon);
	return weapon;
    }
    
    #endregion
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
OnValueChange
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
## Declarations

Declare each variable on a new line.

Good

```c#
int noOflevels;

int currentLevels;

int count;
```

Bad

```c#
int noOflevels, currentLevels, count;
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

## Member Naming Guidelines
# Methods
Use verb noun combinations for methods. 

Good
```c#
CreateEmployee

AddWeapon

InitialiseProjectile
```

Bad
```c#
EmployeeCreate

WeaponAdd

ProjectileInitialise
```
# Fields
1. Don't use underscores
2. Avoid abbreivations
3. Following case guidelines
4. bool members can be prefixed with is or has i.e. isReady, hasFired,
5. Events should be prefixed with On i.e. OnFire, OnMove
6. Do not prefix methods with On, save that for events - see 5. above 

Good
```c#
Weapon weapon

HomingProjectile homingProjectile

public event Action OnFire;
```

Bad
```c#
Weapon _myWeapon;

HomingProjectile hp;

public event Action Fire;
```

## Commenting

1. Single space before the start of the comment

Good 

```c#
// this is a comment
```

Bad

```c#
//this is a comment
```

## Spelling
Use US English spelling.

## TASKS
```c#
// FIXME: reminder/call to fix
// TODO: reminder to complete something
// HACK: temporary fix
```
