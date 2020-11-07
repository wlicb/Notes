### **Week 1: Starting to Program**

1. Documentation of Console Class: 

   ```c#
   using System;
   public class Example { 
      public static void Main() 
     { 
   ​    Console.Write("Hello "); 
   ​    Console.WriteLine("World!"); 
   ​    Console.Write("Enter your name: "); 
   ​    String name = Console.ReadLine(); 
   ​    Console.Write("Good day, "); 
   ​    Console.Write(name); 
   ​    Console.WriteLine("!"); 
     } 
   } 
   // The example displays output similar to the following: 
   //    Hello World! 
   //    Enter your name: James 
   //    Good day, James! 
   ```

2. Using Visual Studio:

   a.   If other languages are selected, be sure to click visual C-Sharp.

3. Structure of Unity C# Code:

   ```c#
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;
   
   public class PrintMessage : Monobehavior
   {
       // Use this for initialization
       void Start()
       {
           
       }
       
       // Update is called once per frame
       void Update()
       {
           
       }
   }
   ```

   a.   The Start method is called when the game object that the script is attached to gets added to the scene.

   b.   The Update method is called once per frame.



### **Week 2: Classes and Objects**

1. Object:

   a.  State: 

   ​	(1) The characteristics of that object.

   ​	(2) Stored in fields in C# (variables inside an object).

   ​	(3) Accessed through properties.

   b.   Behavior:

   ​	(1) What can be done to the object.

   ​	(2) What can be told to the object do to itself.

   ​	(3) Accessed through methods (functions).

   c.   Identity:

   ​	(1) Memory address.

   ​	(2) Determine how to distinguish different objects.

   ​	(3) Created when creating a new object by instantiation.

2. Class:

   a.   Temp-let for creating objects.

   b.   Define the fields, properties and behaviors of every object of the class.

   c.   Object is the actual instance of the class in memory, each object stores its own state.

   d.   Objects defined in the class are all reference variables.

   ![image-20201029203033620](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201029203033620.png)

3. Using a class:

   a.   Constructor:

   ​	(1) Used for instantiation of objects of the class.

   ​	(2) Syntax:

   ```c#
   <class_name> <object_name> = new <class_name> ();
   ```

   b.   Property:

   ​	(1) Syntax of a property in a class:

   ```c#
   <accessibility> <data_type> <property_name> { get; set}
   ```

   ​	“get” means we can read it, “set” means we can write it, “get; set” means we can do both.

   ​	(2) Syntax of accessing the property:

   ```c#
   <variable_name> = <object_name>.<property_name>;
   ```

   c.   Methods:

   ​	(1) Syntax of a method in a class: 

   ```c#
   <accessibility> <return_data_type> <method_name> (<parameter_data_type> 	<parameter_name>)
   ```

   ​	(2) Call the method:

   ```c#
   <return_variable> = <object_name>.<method_name> (<parameter>);
   ```

   ​	(3) For calling method: use `<class>.<method>` if method is a static method (eg. `Console.WriteLine`), 	use `<object>.<method>` if it is not a static method to call it on a particular object.

   ```c#
   // create and print a deck of cards
   Deck deck = new Deck();
   deck.Print();
   
   //access an print Empty value
   Console.WriteLine("Deck Empty: " + deck.Empty);
   
   // shuffle the deck
   deck.Shuffle();
   
   // cut the deck
   deck.Cut(26);
   deck.Print();
   
   // take top card
   Card card = deck.TakeTopCard();
   ```

4. In Unity:

   a.   As a general rule, the scripts that we write in Unity are classes. And when we attach a script as a component to a game object in a Unity scene, then we get an instance of the class, specifically an object attached to that game object.

   b.   In Unity we tend not to use constructors to build instances of classes.



### **Week 3: Unity 2D Basics and Selection**

1. Sprite and Game Object:

   a.   Sprite:

   ​	(1) Graphical asset included in the game.

   ​	(2) Can be single or multiple frames (sprite sheets or sprite strips for animation).

   ​	(3) Can be various formats including .jpg, .png and can be added by dragging into the project folder 	and added to the scene by dragging into the hierarchy window.

   ​	(4) Can be zoomed when clicking on in the hierarchy window.

   ​	(5) Rendered by the Sprite Renderer.

   b.   Game Object: Entity in a Unity Scene.

2. 2D Physics

   a.   Rigid Body Physics:

   ​	(1) There is gravity by default in Unity physics, which can be modified in the Project Settings menu.

   ​	(2) Make the body moving: Applying a force using the method

```c#
public void AddForce (Vector2 Force, ForceMode2D.mode)
```

​				Mode contains Force and Impulse.

​			(3) `GetComponent<type>` is a generalized method used to get the other components attached to 				the object that the script is attached to.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Mover : Monobehavior
{
    // Use this for initialization
    void Start()
    {
        //get the game object moving
        RigidBody2D rb2d = GetComponent<Rigidbody2D>();
        rb2d.AddForce(new Vector2(1,0), 
            ForceMode2D.Impulse);
    }
}
```

​		b.  Collision

​			(1) Collision Detection:

​					(a)  Detecting collisions between game objects.

​					(b) If both objects have 2D colliders, the Physics 2D engine automatically does collision detection.

​			(2) Collision Resolution:

​					(a)  Doing something based on the fact that the collision has been detected.

​					(b) 2D Physics materials for the game object colliders determine how the Physics 2D engine resolves the collision.

​					(c)  Additional resolution can be defined by using the method

```c#
void OnCollisionEnter2D(Collision2D coll) { }
```

​			(3) Collider:

​					(a)  Can be added as a component, many kinds included such as box 2D collider, edge collider (can be added to the edge of the main camera).

​					(b) Size can be adjusted by “Edit Collider” in inspector.

​					(c)  Physical materials can be added to the colliders by creating a Physical Material 2D material and change the friction and bounciness and change the material of the collider to it.

3. Prefab

   ​	a.   A prefabricated game object.

   ​	b.   Advantages:

   ​		(1) Easily adding instances of the prefab to a scene in the editor.

   ​		(2) Easily adding instances of the prefab to a scene from script (spawning).

   ​	c.   Can be added by creating a prefab folder and drag things to it to make them prefabs.

4. Selection

   ​	a.   Timers:

   ​		(1) Usage in game development:

   ​				(a)  Levels with time limits.

   ​				(b) Deciding when to spawning something.

   ​				(c)  Game object with a specific life span.

   ​				(d) Deciding when to increase difficulty of the game.

   ​		(2) Script:

   ​				(a)  Fields:

```c#
	#region Fields
	
	// timer duration
	float totalSeconds = 0;
	
	// timer execution
	float elapsedSeconds = 0;
	bool running = false;
	
	// support for Finished property
	bool started = false;
	
	#endregion
```

​					(b)  Properties:

```c#
	#region Properties
	
	/// <summary>
	/// Sets the duration of the timer
	/// The duration can only be set if the timer isn't currently running
	/// </summary>
	/// <value>duration</value>
	public float Duration
    {
		set
        {
			if (!running)
            {
				totalSeconds = value;
			}
		}
	}
	
	/// <summary>
	/// Gets whether or not the timer has finished running
	/// This property returns false if the timer has never been started
	/// </summary>
	/// <value>true if finished; otherwise, false.</value>
	public bool Finished
    {
		get { return started && !running; } 
	}
	
	/// <summary>
	/// Gets whether or not the timer is currently running
	/// </summary>
	/// <value>true if running; otherwise, false.</value>
	public bool Running
    {
		get { return running; }
	}

    #endregion
```

​					(c)  Methods:

```c#
    #region Methods

    /// <summary>
    /// Update is called once per frame
    /// </summary>
    void Update()
    {	
		// update timer and check for finished
		if (running)
        {
			elapsedSeconds += Time.deltaTime;
			if (elapsedSeconds >= totalSeconds)
            {
				running = false;
			}
		}
	}
	
	/// <summary>
	/// Runs the timer
	/// Because a timer of 0 duration doesn't really make sense,
	/// the timer only runs if the total seconds is larger than 0
	/// This also makes sure the consumer of the class has actually 
	/// set the duration to something higher than 0
	/// </summary>
	public void Run()
    {	
		// only run with valid duration
		if (totalSeconds > 0)
        {
			started = true;
			running = true;
            elapsedSeconds = 0;
		}
	}
	
	#endregion
```

​				(3)  Calling a timer: in the start method: 				

```c#
/// <summary>
    /// Use this for initialization
    /// </summary>
    void Start()
    {
		// create and run timer
		timer = gameObject.AddComponent<Timer>();
		timer.Duration = 3;
		timer.Run ();

		// save start time
		startTime = Time.time;
	}
```

​		b. Spawning

​			(1) Make the objects available in the inspector: using `[SerializeField]`

​			(2)  Defining `Vector3` location to put in the screen location of the object.

​			(3) Using `Vector3 worldLocation = -Camera.main.ScreenToWorldPoint(location);` to convert to world location.

​			(4)  Using `Camera.main.transform.position.z` to represent the z=0 coordinate.

​			(5) `SpriteRenderer` is a type that render the sprite.

​			(6)  `Random.Range(a,b)` contains lower bound a but not upper bound b.

​			(7)  `Instantiate(prefab_name) as GameObject` generates a new instance of the prefab in the scene.

​			(8)  `game_object.transform.position` returns the position of the game object.

```c#
// needed for spawning
[SerializeField]
GameObject prefabTeddyBear;

// saved for efficiency
[SerializeField]
Sprite teddyBearSprite0;
[SerializeField]
Sprite teddyBearSprite1;
[SerializeField]
Sprite teddyBearSprite2;

/// <summary>
/// Spawns a new teddy bear at a random location
/// </summary>
void SpawnBear()
{
    // generate random location and create new teddy bear
    Vector3 location = new Vector3(Random.Range(minSpawnX,maxSpawnX),
                                  Random.Range(minSpawnY,maxSpawnY),
                                   -Camera.main.transform.position.z);
    Vector3 worldLocation = Camera.main.ScreenToWorldPoint(location);
    GameObject teddyBear = Instantiate(prefabTeddyBear) as GameObject;
    teddyBear.transform.position = WorldLocation;
    
    // set random sprite for new teddy bear
    SpriteRenderer spriteRenderer = teddyBear.GetComponent<SpriteRenderer>();
    int spriteNumber = RandomRange(0,3);
    switch (spriteNumber)
    {
        case 0:
       		spriteRenderer.sprite = teddyBearSprite0; break;
        case 1:
       		spriteRenderer.sprite = teddyBearSprite1; break;  
        case 2:
       		spriteRenderer.sprite = teddyBearSprite2; break;
    }
    	
}
```

​		c. Tagged Destruction

​			(1) A game object can be tagged in the inspector “Tag” menu and is there is no suitable tag, a new tag can be added.

​			(2) First spawn game objects: generalized method to instantiate the object:

```c#
GameObject teddyBear;
int prefabNumber = Random.Range(0,3);
if (prefabNumber == 0)
{
    teddyBear = Instantiate<GameObject>(prefabYellowTeddyBear, 
                                        worldLocation, Quaternion.identity); 
}
else if (prefabNumber == 1)
{
    teddyBear = Instantiate<GameObject>(prefabGreenTeddyBear, 
                                        worldLocation, Quaternion.identity); 
}
else
{
    teddyBear = Instantiate<GameObject>(prefabPurpleTeddyBear, 
                                        worldLocation, Quaternion.identity); 
}
```

```c#
`Instantiate<type>(prefab, location, rotation)`
```

`Quaternion.identity` means no rotation.

​				(3) Using timer to destroy: In the Destroyer script: call the timer in the Start method and in the Update method:

```c#
/// <summary>
/// Update is called once per frame
/// </summary>
void Update()
{
    // check for timer finished and restart
    if (explodeTimer.Finished)
    {
        explodeTimer.Run();

        // blow up C4 teddy bear
        GameObject teddyBear = GameObject.FindWithTag("C4TeddyBear");
        if (teddyBear != null)
        {
            Instantiate<GameObject>(prefabExplosion,
                teddyBear.transform.position, Quaternion.identity);
            Destroy(teddyBear);
        }
    }
}
```

`GameObject.FindWithTag(“string”)` is used to find an object with certain tag.



### **Week 4: Unity Input**

1. Mouse Input:

   a. Mouse location processing: `Input.mousePosition` accesses the screen position of the mouse. 

   ```c#
   // Update is called once per frame
   void Update()
   {
       // convert mouse position to world position
       Vector3 position = Input.mousePosition;
       position.z = -Camera.main.transform.position.z;
       position = Camera.main.ScreenToWorldPoint(position);
   
       // move character to mouse position
       transform.position = position;
       ClampInScreen(); // To be explained in next few lines
   }
   ```

   b. Clamp the game object (keep the object within the screen): 

   ​	(1) Define class `ScreenUtils` to calculate the information of the screen:

   ​			Fields: `screenLeft, screenRight, screenTop, screenBottom`

   ​			Properties: the same

   ​			Method: `Initialize`: to initialize the game screen:

   ```c#
   // Initializes the screen utilities
   public static void Initialize()
   {
   	// save screen edges in world coordinates
   	float screenZ = -Camera.main.transform.position.z;
   	Vector3 lowerLeftCornerScreen = new Vector3(0, 0, screenZ);
   	Vector3 upperRightCornerScreen = new Vector3(
   			Screen.width, Screen.height, screenZ);
   	Vector3 lowerLeftCornerWorld = 
   			Camera.main.ScreenToWorldPoint(lowerLeftCornerScreen);
   	Vector3 upperRightCornerWorld = 
   			Camera.main.ScreenToWorldPoint(upperRightCornerScreen);
   	screenLeft = lowerLeftCornerWorld.x;
   	screenRight = upperRightCornerWorld.x;
   	screenTop = upperRightCornerWorld.y;
   	screenBottom = lowerLeftCornerWorld.y;
   }
   ```

   ​	(1) Initialize the game screen in `Awake()` method in the `GameInitializer` script (class).

   ​	(2) Defining a `ClampInScreen()` function to determine whether it is out of screen.

   c. Mouse Button Processing:

   Using `public bool Input.GetMouseButtonDown(int)` method

   int = 0: left

   int = 1: right

   int = 2: middle

2. Input Manager

   a.  Advantages:

   ​	(1) Let us map named input axes to particular inputs.

   ​	(2) Let us check for input in our scripts.

   ​	(3) Let players remap the input axes when they play.

   b.   Can be accessed by “Project Settings > Input”.

   c.    In “Build Settings”, we can build the game and after this, the input axes can be changed in the “Input” menu by double-clicking the entry and press the button we want to change to.

   ![image-20201029215821151](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201029215821151.png)

   d.   Mouse button input can be achieved in the input manager by adding a new axes and set the positive button to be “mouse 0”, and use the `Input.GetAxis(string)` method and if returns larger than 0, it means that the “mouse 0” button is clicked. However, this can cause the problem that clicking the mouse may last several frames while the update method works every frame. This can be solved by adding a `bool` variable `previousFrameChangeCharacterInput = false`, and make it true when the first frame of mouse click is called.

   ```c#
   // Update is called once per frame
   void Update()
   {    
       // change character on left mouse button
       if (Input.GetAxis("ChangeCharacter") > 0)
       {
           if (!previoudFrameChangeCharacterInput)
           {
               previousFrameChangeCharacterInput = true;
               // save current position and destroy current character
           	Vector3 position = currentCharacter.transform.position;
           	Destroy(currentCharacter);
   
           	// instantiate a new random character
           	int prefabNumber = Random.Range(0, 4);
           	if (prefabNumber == 0)
           	{
               	currentCharacter = Instantiate(prefabCharacter0, 
                   	position, Quaternion.identity);
               }
               else if (prefabNumber == 1)
               {
                   currentCharacter = Instantiate(prefabCharacter1, 
                       position, Quaternion.identity);
               }
               else if (prefabNumber == 2)
               {
                   currentCharacter = Instantiate(prefabCharacter2, 
                       position, Quaternion.identity);
               }
               else
               {
                   currentCharacter = Instantiate(prefabCharacter3, 
                       position, Quaternion.identity);
               }
           }
       }
   }
   ```

   3. Keyboard Processing:

      a.   Can be achieve with the input manager “horizontal” “vertical” and other axes. The following example uses it to let the character in the game to move around with the speed of `MoveUnitsPerSecond`.

      b.   Keyboard control can also be added as an alt positive/negative button.

      ```c#
      // Update is called once per frame
      void Update()
      {
          // convert mouse position to world position
          Vector3 position = Input.mousePosition;
          float horizontalInput = Input.GetAxis("Horizontal");
          float veriticalInput = Input.GetAxis("Vertical");
          if (horizontalInput != 0)
          {
              position.x += horizontalInput * MoveUnitsPerSecond *
                  Time.deltatime;
          }
          if (verticalInput != 0)
          {
              position.y += verticalINput * MoveUnitsPerSecond *
                  Time.deltatime;
          }
      }
      ```

      

