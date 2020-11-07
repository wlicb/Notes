### **Week 1: Arrays, Lists, and Iteration**

1. Arrays:

   a.   Can be used to include multiple game objects

```c#
[SerializeField]

GameObject[] prefabCharacters = new GameObject[4]
```

​		b.   After defining the array, the size and elements can be modified in the inspector.

![image-20201030165203531](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20201030165203531.png)

​		c.   Populate array with characters:

```
profabCharacters[0] = (GameObject)Resources.Load(“Character0”);
```

`Resource.Load` returns object while `prefabCharacters[0]` is a game object, so conversion between object and game object is needed.

Make sure that these prefabs are under the `Resources` folder directly if this method is used. Use `@“prefab\Character0”` if the `Character0` is under `Resources\prefab`.

2. Lists: 

   a.   Disadvantage of array: have to know the size of the array when defining.

   ​		Advantage of list: no need to define the size.

   b.   One list can only store one data type.

   c.   Can be generated in the following way:

```c#
List<GameObject> prefabCharacters = new List<GameObject>();
```

`List` is the generic and `GameObject` is the data type.

​		d.   Can add an element into the list by using the method

```c#
prefabCharacters.Add((GameObject)Resources.Load(“Character0”));
```

​		e.   Elements can be accessed exactly the same as arrays.

​		f.   Elements can be deleted by using the method

```c#
GameObject pickup;

pickups.Remove(pickup);
```

​		g.   List has a `Count` property to get the number of elements inside the list.

​		h.   List can be added a array by using the `AddRange` method.

```c#
gameObjects.AddRange(Object.FindObjectsOfType<GameObject>());
```

`			FindObjectsOfType` method can find all the objects of certain type in the game.

​		To simplify, using tag is a great method.

```
gameObjects.AddRange(GameObject.FindGameObjectsWithTag(color.ToString()))
```

  	 The input of method ~ is string, so the input should be converted to string.

​		i.   `position.Normalized();` gets the unit vector.

3. Iteration:

   a.   DLL can be used to use a namespace written by others without the source code.

   b.   Foreach Loops: 

   ​	(1) Syntax:

```c#
foreach (datatype variable_name in list_name)

{ }
```

​			Example:

```c#
// print cards in the hand
foreach (Card card in hand)
{
    Console.WriteLIne(cark.Rank + " of " + 
                      card.Suit);
}

// add 5 cards to hand
for (int i = 0; i < 5; i++)
{
    hand.Add(deck.TakeTopCard());
}

// print cards in the hand
Console.WriteLine();
foreach (Card card in hand)
{
    Console.WriteLine(cark.Rank + " of " +
                     card.Suit);
}
```

​			(1) Foreach loops can be used when all the elements in the loop will be executed but if not, then `foreach` loop is no longer useful.

​			(2) Modifying the elements in the list is not allowed in `foreach` loop, so it can’t be used to remove certain element.

​		c.   Using while loop to make sure collision-free spawning

​		Using a while loop to determine if it is overlapping using `Physics2D.OverlapArea(min, max)` method as well as using another parameter to determine when to timeout.

```c#
// make sure we don't spawn into a collision
		int spawnTries = 1;
		while (Physics2D.OverlapArea(min, max) != null &&
		spawnTries < MaxSpawnTries)
		{			
			// change location and calculate new rectangle points
			location.x = Random.Range(minSpawnX, maxSpawnX);
			location.y = Random.Range(minSpawnY, maxSpawnY);
			worldLocation = Camera.main.ScreenToWorldPoint(location);
			SetMinAndMax(worldLocation);

			spawnTries++;
		}
		
		// create new bear if found collision-free location
		if (Physics2D.OverlapArea(min, max) == null) {
			GameObject teddyBear = Instantiate(prefabTeddyBear) as GameObject;
			teddyBear.transform.position = worldLocation;

			// set random sprite for new teddy bear
			SpriteRenderer spriteRenderer = teddyBear.GetComponent<SpriteRenderer>();
			int spriteNumber = Random.Range(0, 3);
			if (spriteNumber < 1)
            {
				spriteRenderer.sprite = teddyBearSprite0;
			}
            else if (spriteNumber < 2)
            {
				spriteRenderer.sprite = teddyBearSprite1;
			}
            else
            {
				spriteRenderer.sprite = teddyBearSprite2;
			}
		}
```



### **Week 2: Abstraction and Console App Class**

1. Abstraction:

   a.   The details that matter in our abstraction are directly related to the problem we’re trying to solve. 

   b.   Abstraction helps to reduce the cost of time, CPU and so on in the coding process.

   c.   The implementation Mechanism: Classes.

2. Console App Class: 

   a.   State: Fields and properties:

   ​	(1)  `#region Fields` (`#region Properties`) and `#endregion` mark the beginning and ending of the field part.

   ​	(2)  Fields can be made private and the access modifier is private by default.

   ​	(3)  Properties can be read or modified using `get { }` and `set { }`. get will return the value of field while set will assign the field to a “value”.

   ​	(4)  Properties use capital letter in the first letter.

   ```c#
   #region Fields
   int numSides;
   int topSide;
   #endregion
       
   #region Properties
   /// <summary>
   /// Gets the number of sides
   /// </summary>
   /// <value>number of sides</value>
   public int NumSides
   {
   	get { return numSides; }
   }
   /// <summary>
   /// Gets the top side
   /// </summary>
   /// <value>top side</value>
   public int TopSide
   {
   	get { return topSide; }
   }
   #endregion
   ```

   b.   Identity: Constructor:

   ​	(1) One type of constructor:

   ​			(a)  In the class: 

   ```c#
   # region Constructors
   public Die()
   {
      numSide = 6;
      topSide = 1;
   }
   # endregion
   ```

   ​			(b) In the program: 

   ```c#
   Die newdie = new Die();
   ```

   ​	(2) Another general type of constructor:

   ```c#
   # region Constructors
   public Die(int numSide)
   {
      this.numSide = numSide;
   }
   # endregion
   ```

   `this` represents the object that it is currently in and avoids conflicts between different variables in different classes with the same name.

   ​	(3) Calling one constructor in another:

   ```c#
   #region Constructors
   /// <summary>
   /// Constructor for six-sided die
   /// </summary>
   public Die() : this(6)
   {
   }
   
   /// <summary>
   /// Constructor for die with numSides sides
   /// </summary>
   /// <param name="numSides">number of sides</param>
   public Die(int numSides)
   {
   	this.numSides = numSides;
   	topSide = 1;
   }
   #endregion
   ```

   Using `this()` method, the compiler will automatically recognize and call another constructor.

   c.   Methods:

   ​	(1) Defining a method in a class: 

   ```c#
   public void Roll () { }
   ```

   ​	(2) Using random in a method: To avoid using the same seed every time, the random number can be generated in the field.



### **Week 3: Unity classes**

1. Using `OnMouseUpAsButton()` method to detect whether the mouse is on the game object and released after pressed down.

   Example in the Fish class: fire the fish

   ```c#
   /// <summary>
   /// fires the fish
   /// </summary>
   void OnMouseUpAsButton()
   {
   	Rigidbody2D rb2d = GetComponent<Rigidbody2D>();
       rb2d.AddForce(new Vector2(0,20), ForceMode.Impulse);
   }
   ```

   This method is returns void and can be added some applications inside it when defining it inside the class.

   2. A `public` method should be defined in the class if it will be called outside the class.



### **Week 4: Strings, Text IO, and Audio**

1. Strings:

   a.   The method `Console.ReadLine()` will read the input of the user and return a string.

   b.   Different strings can be combined in the Console.WriteLine() method:

```c#
Console.WriteLine(“Game Tag: ” + gameTag);
```

​		c.   Strings can not be changed once defined and should be manipulated by using the `StringBuilder` class to do that.

​		d.   `Console.Write()` will not generate the next line while `Console.WriteLine()` will.

​		e.   Find the location of a character of a string: Use the `IndexOf` method, return the index if it is in the string and return -1 otherwise.

```c#
int commaLocation = string.IndexOf(‘,’);
```

​		f.   Extract from a string: Use the Substring method with the parameter of the start index and end index of the substring.

```c#
string substring = string.Substring(0, commaLocation);
```

​		g.   String of number can be converted to float using Parse method:

```c#
float percent = float.Parse(substring);
```

2. Text input and output

   a.   Text output:

   ​	(1) To achieve text output in the game, a Canvas should be created inside the UI menu. After creating a Canvas, a Text need to be created inside the UI menu.

   ​	(2) Remember that a variable needs to be `[SerializedField]` to be seen in the inspector. A Text object needs to be declared and this kind of object is under namespace of `UnityEngine.UI`.

   ​	(3) The script can be attached to the Canvas to make changes to the text.

   ​	(4) An int can be converted to string using `int_name.ToString()` method.
   
   ​	Example: Scoring support in the fish shooting game:

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
/// <summary>
/// The HUD
/// </summary>
public class HUD : MonoBehaviour
{
    // scoring support
    [SerializeField]
    Text scoreText;
    int score;
    const string ScorePrefix = "Score: ";
	/// <summary>
	/// Use this for initialization
	/// </summary>
	void Start()
	{
        scoreText.text = ScorePrefix + score.ToString();
	}
    /// <summary>
    /// Adds the given points to the score
    /// </summary>
    /// <param name="points">points</param>
    public void AddPoints(int points)
    {
        score += points;
        scoreText.text = ScorePrefix + score.ToString();
    }
}

```

​			(6) The content of the text can be modified in the `text_name.text` field.

​		a.   Text input:

​			(1) A `InputField` can be added to Canvas to enable text input.

​			(2) Script can be attached to the main camera and populate it with the `InputField` component.

3. Audio

   a.   Component Audio Source can be added and attached to the object to create audio. Inside the Audio Source, Audio Clip should be added. By default, the sound is played one when wake up.

   b.   Script should be added to manage the sound. Method `audioSource.Play()` can be used to play the sound.

   c.   Audio Manager:

   ​	(1) To avoid the audio source being destroyed after one object is destroyed, a single game audio source should be used to play all the sound and an audio manager should be applied to it.

   ​	(2) Dictionary can be initialized and it can protect the game from file name changes as if the file name is changed then only the code in the dictionary should be modified.

   ```c#
   Dictionary<AudioClipName, AudioClip> audioClips = new Dictionary<AudioClipName, AudioClip>();
   ```

   

   Dictionary elements can be added by this method:

```c#
audioClips.Add(AudioClipName.BurgerDamage, Resource.Load(“BurgerDamage”));
```

​			(3) `PlayOneShot` method is a way of “play and forget” of audio. This is used in one single audio source object to make the audio be able to overlap. `Play` method will be implemented until the end of the audio, which is not what is needed to overlap different audio.

