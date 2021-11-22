# Input

> I/

Alright let’s get our player sphere responding to input.

Quick side note, Unity has “recently” created a new input system that they are trying to switch over to. It has a lot of cool features and can do some really powerful things… but we are not going to use it for this tutorial, mainly because it’s kind of a pain in the ass sometimes and way more complicated than we need right now. I’ll leave some links for how to use it at the end if you really want to, but I suggest starting with the old methodSide note over.

Input in Unity needs to be checked constantly. We need to always be checking whether or not certain keys have been pressed or released. As such, a good candidate for where to put it would be in the Update function. It would actually be easier to put it in the FixedUpdate function (as that is where we will put our movement code), but it’s not as good a practice. The reason is that Update usually runs more often than FixedUpdate. So, if you press a key, Unity can react to it faster if it’s in Update. It can even miss keypresses in FixedUpdate if you are using specific functions for your input.
A better practice is to check for input in Update, then set a flag (boolean variable). Then in FixedUpdate, you respond to that flag and apply the forces.

Unity has a built-in function for checking for input. You give it the key or mouse button as a parameter, and it returns a boolean for whether that button was pressed.
To get the right Arrow key, you write this: `Input.GetKey(KeyCode.RightArrow)`.

There are other functions like `GetKeyDown()` and `GetKeyUp()`, which are similar.Getkey returns true while a key is pressed. `GetKeyDown()` and `GetKeyUp()` only returns true the exact frame the key is pressed down or up, which is why you can miss them in FixedUpdate. For now, let’s stick with GetKey though.
Make an If Statement in the Update function that prints “right” if you press the right arrow key. Then test it to see if it works.

If you got that to work, then let’s change it up a little, instead of printing right, let’s set a boolean flag. reate a boolean variable below your Rigidbody variable like this:

```c#
private bool pressedRight = false;
```

Note that we initialize it to `false`. We could also leave it uninitialized, but we would need to make sure we set it before it gets used (like in the start method, for example).

Now, in your if statement, set it to true. You should also create an else block where you set it to false so that it resets when you release the key.

Now, in your FixedUpdate method, check if the boolean is true. If it is, go ahead and add your movement to the right like before. You should be able to move the sphere now, but only when you press the right arrow key.



Now repeat this for all cardinal directions. For the up and down arrow, make your sphere move in the `z` direction,  i.e: change the 3rd value in the Vector3.

Now by this point, the update function is looking a little cluttered. Update is a very important and often used function. So we want it to be as clean as possible. Let’s move this to a new function called `CheckInput()`.

```c#
private void CheckInput() 
{
	if (Input.GetKey(KeyCode.RightArrow)) pressedRight = true;
  else pressedRight = false;
  
  if (Input.GetKey(KeyCode.LeftArrow)) pressedLeft = true;
  else pressedLeft = false;
  
  if (Input.GetKey(KeyCode.UpArrow)) 	pressedUp = true;
  else pressedUp = false;
  
  if (Input.GetKey(KeyCode.DownArrow)) pressedDown = true;
  else pressedDown = false;
}
```

> You can simplify your if statements by removing the { } if there is only 1 line in each. Be **VERY** careful that you don’t accidentally add another line in because that will cause errors

Similarly, you should probably do the same for the If statements in `FixedUpdate`. Let’s move that to a new function as well.

```c#
private void ApplyForces() 
{
	if (pressedRight) rb.AddForce(1f, 0f, 0f);
  if (pressedLeft) rb.AddForce(-1f, 0f, 0f);
  if (pressedUp) rb.AddForce(0f, 0f, 1f);
  if (pressedDown) rb.AddForce(0f, 0f, -1f);
}
```

Much better. Give it a try in game and see how it looks. You should be able to move left/right and forward/backward with the arrow keys now.

Now, at this point, I realized I made an error when naming my variables. So rather then re-taking all my screenshots, I’ll use this opportunity to show you how to rename variables in Visual Studio. 
Right click the variable you want to rename and select Rename. You should then be able to move the cursor around and delete/add letters as you need. This will automatically rename all instances of a variable. It also has some extra options in the top left you may want to look at as well.

![img](https://lh6.googleusercontent.com/sjEeMFxDpB3t-9qi4j3qaBTMZo8dxfYYYzvawxPV4fFY5EY0KYMvNqpU9fvqSVHSRUd4sC1uCrBDKcpXsQRViE1Ml1h-Ghj4rZYDFRUolxqjg_QvSQO0fUtCALj7K7bdM6rNLPl8dZJU)

![img](https://lh4.googleusercontent.com/7QkncbnEuYUS7KvbqxAGXeQt9X9cLGj8a4Uxtjw7OEWF6c0MKgPDzP82IFna7HWwd7qRqulgBKu9qZsQ1nB83jTR3U32j5S85Vw50eM2WvIEF911DQSUrYvKMnixz4x4DgqU_7GGIcl1)

They should look like this instead. It’s a convention thing:

```c#
private bool isPressingRight = false;
private bool isPressingLeft = false;
private bool isPressingUp = false;
private bool isPressingDown = false;
```

Now, from our current angle, this is all a little hard to see, so we’re going to whip up a camera movement script to make our player movement easier to see.
Make a new C# script called `CameraMovement.cs` and add it to the Main Camera GameObject that Unity made for us. 

Before we move on, lets change our camera’s angle a bit:

![img](https://lh5.googleusercontent.com/I9mEDkCOCXUXix2OFmeBU7kwgz3ozuIMAwCGOpfNdzEJwzOb3x_wjkOTX0FNKwDQK22_sybGeaLLC_spnKocUhMI6Jx-XE8J0mSZHtyiOj2KIi7U72zCSEen_2IHPFRYdkRG_XLdkAJy)

Now we’re back a bit and looking down at the ball. But it’s still hard to see given the background. Let’s make a ground object for it to sit on. 
Add a plane Object by right clicking in the hierarchy and going under 3D object. 

We can go and rename that to Ground and reset the transform on it so it’s below the ball, and then make it twice as big.

![img](https://lh3.googleusercontent.com/bUWVKOEsuM8263cS2mbvj6DK09kZdBZWin23gep04ewms5ItHSYSR8_tW8sdEypE6XIlcAWzJpZQND_BoQq_RsvPjWKUYkrBD3-j69wWqZfONUZAt6nTvl9ENKPHerNPdAsor3guuVWV)

![img](https://lh6.googleusercontent.com/hyPk2M9kwnrTZ-TOyUSubrq1RdNHfFSDne4G725eRUPlpo52k0WuPMd9Ma3AUOXUOxdY_3ckC_ciz0m9r1rSdP4uLYXyoNCAgJ6i6lNn7vuJv8PiRqS6YEccsqYPfiwMsAkg1G7JJcGH)



Now this plane is currently cutting through the middle of our sphere, so we should fix that. I think it makes the most sense to raise the sphere up to sit on the plane, so that our ground is at a height of 0. Now, what you want to do is set the Y value of the sphere to 0.5. This is because the sphere has a size of 1, so raising it by half of that will put the bottom of the sphere at y level 0.

![img](https://lh6.googleusercontent.com/QC53RsjxCPUXQJju82pERSiow4r3_Q-w2EP5_ZopIjVTwAp6cuwW26adH69htxi5n-1u_AaseiPJQx5cuXWn37W3vL-aJbmIswxPDUZuslmOME12oQ6y8KiXMmMCSXBN0i1QZTAIYqni)

This is still hard to see though, since they are the same color, so let’s change that. To change the color of an object, we need to give it a material with that color. If you remember when we created the sphere, we gave it a material, the default material. To change it, we need to create a new one. 
Right click in the *Project window* and select Create -> Material. 
I named mine PlayerMaterial, since I’m going to put it on the player. If you want to change the color of the ground, that works too. If you select it, you’ll see it has an option called Albedo. If you select the white box next to it, a color picker will pop up and you can choose any color you'd like. 

![img](https://lh3.googleusercontent.com/lgzBgAD94FiU2SCxyg30Sme81lpn0JW0ylPPzUeLSrTRqsE5dN6h1aPx-paq5mQGA129tyHvlYekyAIH2QME4hoXAerWAiXC3p3NOYSxRZI--IGZfkfW0wg-u5v6x2MoB_96gXZXs4AG)

![img](https://lh6.googleusercontent.com/4ha8J6uFLdRT8GVN98jghsX8MTIbeK0q20gvhnexnAtOjs0pms8V99ttg8C6PBDsLNobnK1v6lyrpfWDfMjKOZKUzl9_NJFGdodVX2rHwQuY7QrDaPhXE6QkDwaM4bqNFC9928ZO2owq)

After you pick a color, you can drag the color directly onto the player (or ground) in the scene to apply it. You could also select it in the mesh renderer like we did before as well.

And now you should have something like this, which is much easier to see:

![img](https://lh5.googleusercontent.com/GSwIu34f-tAh2-kak_jviB5JWYpfoJxuQLFVibqR8pyI92zUFsBLTp4hrqX4Y_3TptR3B-Dy9FJoXJ6monDAOnGMxPA7NwHSPp9XwNlZmzRDHlp5dqRa3PATYsqhYEFRRfJ7pDrpRh15)

Go ahead and play it again to see how it looks.

You may want to adjust the speed at this point. You could go into the playermovent script and keep changing the value there and replaying the game, but that’s tedious and hard to do. Instead, lets store the speed as a variable and change it in the inspector.

Create a float called speed and make it appear in the inspector `[SerializeField]` with the `[SerializeField]` attribute. Then replace your hard coded `private float speed;` values that you use in the `AddForce()` calls.

Now we should be able to see it in the inspector. And even better, we can edit it while the game is playing. Remember that the values we give it while the game is playing do not stick around, so you’ll have to re-apply your changes later. 

Regardless, this is much faster and easier to fine tune than keeping the value in your script. So go ahead and find a speed you like. 

Now that we have a ground, let’s also add gravity back in. Remember, it’s a setting in the Rigidbody of the player. 
Let’s also do some housekeeping and make slime folders for our assets. I made one for my scripts and another for materials.

![img](https://lh6.googleusercontent.com/eZkUMLvNBbQVqXAtPHk8RSbCK0zjPzKXt3EaU7OUd_UCpdlPf3mCMEZVLTxo88F2wN-qLV3xOEN3DKo7of3djU0_XrGbQA3G1Dp2zMDE0f9D1G71ouM1WAyzuGwYYc6pO1zeZygfxE-u)

You may find the scripts close in Visual S tudio after you do this. Let’s open both of them up again and start writing the camera movement script. 

The type of effect we are trying to make is to get the camera to move with the player. Now, we could just copy and paste our movement code on the camera, but that’s messy and inefficient and would involve us putting a Rigidbody on the camera as well. Instead, we can just borrow the changes in movement that we already calculated.

Essentially we just move our camera however much our player moved each frame.

We start by getting a reference to the transform of our player. Create a private variable of type Transform to store it.

Then, in the start method of the Script, we need to get it. Now, the camera is on a different object from the player, so getting the component we need is a little trickier. There are a couple of methods for doing this, each has their own strengths, but for now we’re going to do it like this. 

There is a function in Unity that is very similar to `GetComponet<T>()`. It’s called `FindObjectOfType<T>()`. You give it a component T just like `GetComponet<T>()`, but instead of searching the current GameObject for the component, it searches every GameObject in the scene for the component.

Since our player is the only GameObject that’s going to have a PlayerMovement script, that is what you should look for. But we don’t need the movement script, we need the transform. So, you need to get the transform from the GameObject with the PlayerMovement script, like this:

```c#
void Start()
{
  playerTransform = FindObjectOfType<PlayerMovement>().transform;
}
```

Note that `FindObjectOfType` returns the type that you give it, not a gameObject.

If you have a script with several instances, there is also `FindObjectsOfType<PlayerMovement>()`, which returns an array of all the found PlayerMovement classes.

> If you have an object with many many instances, this method is not recommended, since parsing through all of them is time consuming. In fact, this function is, in general, time consuming. So, it is recommended you do not use it in an update method. You should instead do it in a start method and store it in a variable like we did here.

Next, we need to get the offset in position between our camera and our player at the start of the game. This way we can calculate the new position of our camera every time the player moves. To do this, we add this offset to the new player position each frame and move our camera to the new position.
We can do this by subtracting the position of our player from the position of our camera. We’re going to need to store this in a variable for later so go ahead and create a Vector3 for this.

```c#
void Start() 
{
  playerTransform = FindObjectOfType<PlayerMovement>().transform;
  offset = transform.position - playerTransform.position; 
}

// Update is called once per frame
void Update()
{
  transform.position = playerTransform.position + offset;
}
```

We can then add this to the player position in the update function and set our cameras transform to the result.

One last thing we have to fix is the function call order. In general. it’s a good Idea to ensure that any reactionary code like our camera movement always happens after the code it’s reacting to. In our case, the movement of the sphere happens in Unity’s physics system loop, directly after every call to `FixedUpdate()` has been called. Then all the calls to Update happen, then there is another function called LateUpdate which gets called. You are guaranteed that all calls to FixedUpdate occur before Update, and similarly for LateUpdate and Update.

Now, since our movement is currently 100% physics-based, we know it always occurs before Update. However, if we ever add any non-physics based movement in an Update function, we can get into a situation where the camera movement code updates the camera position based on the previous player position. This is because there are no guarantees about the order of calls to Update functions. And if this happens, we would get a jitter in our movement. As such, we should change our Update function to a LateUpdate function so we don’t have to worry about this. 

If you want more info on the Update loop and the order of operation is in Unity, you can find it here: https://docs.unity3d.com/Manual/ExecutionOrder.html#UpdateOrder
It’s a bit complicated and more has more info than you need right now though, so I’d only give it a quick skim until after you complete the rest of the tutorials.