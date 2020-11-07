### **Week 1: Exceptions and file IO**

1. Exceptions:

   a.   Exceptions represent errors in the code. 

   b.   Handling exceptions:

   ​	(1) Put the code that may cause the exceptions into `try{ }`.

   ​	(2) Use `catch(Exception exception_name)` method to catch the information of exception.

   ​	(3) We can also catch the excepts in more detail such as `catching(FormatException fe)`

   ​	(4) After determining all the exceptions we want to catch, we can use `finally{ }` to show that we have completed the exception handling process.![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

2. File IO:

   a.   After completing processing the file, try, catch and finally block should be added to make sure that it does not crash the program.

   b.   Namespace `System.IO` is needed to do file IO.

   c.   File output:

   ​	(1) To create a file output stream:

```c#
StreamWriter output = null;
```

​			(2) To create a new file: 

```c#
output = File.CreateText(“OneStepCloser.txt”);
```

​			(3) To write line in the output file:

```c#
output.WriteLine(“This is a line”);
```

​		d.   File input:

​			(1) To create a file input stream:

```c#
StreamReader input = null;
```

​			(2) To input into the file:

```c#
line = input.ReadLine();
```

​		e.   To close a file:

```c#
input.Close();
```

​		f.   Game Configuration Data Files:

​			(1) To let the game designers tune the game without changing the code.

​			(2) There are mainly two kinds of game configuration data files:

​					(a)  Comma-Separated Value(CSV) files:

​							Easily exported from spreadsheets.

​							Harder for people to read the raw file.

​					(b) Extensive Markup Language(XML) files:

​							Easier for people to read the raw file.

​							Should build a custom XML editor.

​			(3) When retrieving the game configuration data, in case that the file reading process fails, default values should be added in the field.

​			(4) We can get the data from the file using:

```c#
input = File.OpenText(Path.Combine(Application.streamingAssetPath, ConfigurationDataFileName);
```

`streamingAssetPath` is a folder used to hold the data file.

​		g.   `PlayPrefs`: A class that stores and accesses player preferences between game sessions.

​		h.   To split a string according to the location of the comma:

```c#
string[] values = csvValues.Split(',');
```

 		Example: Text Output:

​			In the main function:

```c#
// write to a text file
StreamWriter output = null;
try
{
	// create stream writer object
	output = File.CreateText("OneStepCloser.txt");
	
    // write a few lines
	output.WriteLine("Everything you say to me");
	output.WriteLine("Takes me one step closer to the edge");
	output.WriteLine("And I'm about to break");
}
catch (Exception e)
{
	Console.WriteLine(e.Message);
}
finally
{
	// always close output file
	if (output != null)
	{
		output.Close();
	}
}
```

​				Text Input:

```c#
// read from the text file
try
{
	// create stream reader object
	input = File.OpenText("OneStepCloser.txt");

	// read and echo lines until end of file
	string line = input.ReadLine();
	while (line != null)
	{
		Console.WriteLine(line);
		line = input.ReadLine();
	}
}
catch (Exception e)
{
	Console.WriteLine(e.Message);
}
finally
{
	// always close input file
	if (input != null)
	{
		input.Close();
	}
}
```



### **Week 2: Inheritance and Polymorphism**

1. Inheritance:

   a.   Inheritance is a way to structure our code so multiple classes can share common fields, properties and methods. Classes can still have class-specific data and operations as well.

   b.   Multiple inheritance is not allowed, which means that we can’t use a child class to be another parent class.

   c.   To define a child class:

```c#
public class child_class : parent_class { }
```

​		d.   To define constructor of the class with the fields of the parent class:

```c#
public child_class(int height, int weight)
    : base(height, weight) { }
```

​		e.   In the parent class, when defining a method, a key word virtual can be used to make the child class be able to override the method:

```c#
public virtual void HaveFun() { }
```

​				In the child class, a key word override will be used and the signature of the method is exactly the same as in the parent method:

```c#
public override void HaveFun() { }
```

​				If in the child class, the method is not mention and the behavior is not changed, then when calling the method for this child, the method will behave as the parent method.

2. Polymorphism:

   ​	a.   Polymorphism means a particular method call can behave differently (take multiple forms) based on the project on which it is called.

   ​	b.   We better avoid using the method defined in the subclass to the objects which belongs to the superclass, and this is especially important for the `foreach` loops.

   ​	c.   All the scripts are child classes of the `MonoBehavior` class. When running the game, we call the method in the child class to operate the logic defined by ourselves.

 

### **Week 3: Event Handling and Menus:**

1. Delegates and event handler:

   a.   Delegates:

   ​	(1) A type that defines the method signature, it is like a pointer to a particular method.

   ​	(2) Used to pass a method as argument to another method.

   b.   Event Handler:

   ​	(1) Methods that respond when an event occurs.

   ​	(2) Can be seen as a kind of delegates.

![img](file:///C:/Users/Lenovo/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)

2. `UnityEvent` and `UnityAction`

   a.   `UnityEvent`:

   ​	(1) A family of classes that provide events for different numbers of parameters and the parameters can be whatever type we want them to be.

   ​	(2) None-argument form: just call all the listeners when the event happens.

```c#
UnityEvent.my_event;
```

​			(3) One or more arguments: We should override the class type.

```c#
public class my_event : UnityEvent<int>;
```

​		b.   `UnityAction`:

​			(1) A family of classes that provide event handlers for different numbers of  parameters and the parameters can be whatever type we want them to be.

​			(2) One argument: `UnityAction` is a delegate class.

```c#
UnityAction<T0> (T0 arg0);
```

​		c.   To implement `UnityEvent` and `UnityAction`, `UnityEngine.Events` namespace should be used.

​		d.   Event Manager:

​			(1)  Making all the objects unaware of each other and handle all the events in the event manager script.

​			(2)  It is not a child class of `MonoBehavior` and it is a `static` class.

