# Movement/Physics 

> GameObject go brrrrr

There are essentially 3 ways to move a GameObject:

- Directly setting the value in the Transform
- Applying forces through a rigidbody
- Animation

We’ll go over the first 2, and which is best when.

![img](https://lh5.googleusercontent.com/tK-CwFx_mDOKnnrsI4Vn85woIgGH5fQ8rY0D-3Q1K6nUQm_Zw8qwn5c_C-Elayoi_BocDJSVUZ0hS7SMactxHPOQkgTk54UUX5l7ykYpVKwmWiLsr7JzkA1zCRdTjoL-J4KMnhVFIts)Let’s start with the transform. Go to our PlayerMovement script and delete the two print statements. Then press play and take note of where the sphere is in the screen (it should be the center of the screen).

Now let’s make some changes. We're going to set the sphere’s transform to be 5 units to the right of where it is now. To do this we need a reference to the transform component. Now, the transform is a special component. Remember how when you created the sphere, the transform was already there? Every GameObject needs to have a transform, so, the transform is actually a variable in our base class that we can access like any other class/instance variable. you just write… transform.
To move the sphere, we need to change the transform’s position. To do that we write `transform.position = `. What we put on the other side is a special Unity object (it’s a struct if you know C) called a Vector3. It is essentially an array with 3 values, an `x`, `y`, and `z` value. I think you can see what those relate to in terms of position. To create a Vector3, write  `new Vector3(5f, 0f, 0f).` (the f just means it’s a float)

Press play again and you should see something like this. 

![img](https://lh6.googleusercontent.com/agllXxUxVijjxN5ROfakapKv8KFp1esIRF0cPTYVK09hGDSvS8M8o6mmznCdVb_x5Ho-FxRklNOEqp3ptjM5q0FoR8Llz6Vp0cUbXAAgBH0MNCp9th9iFpHVNEDoa5RFBygd4w098WE)

And if you select the sphere in the hierarchy and look at the transform in the inspector, you should see its position has updated accordingly.

Now let’s try it in Update instead. To make this work, we're gonna want to reduce the distance. Like, a lot. In a game with this little stuff in it, update is likely running hundreds if not thousands of times a second. So let's comment out the line in start and copy it over to Update. For the one in update, we’ll need to change the following: 

Instead of setting the transform to 1 value, we’ll need to accumulate a new value. So instead of setting it equal to our new Vector3, use the += operator. You should also reduce the number by about 3 degrees of magnitude.

You should see the ball glide across the screen. 

Feel free to experiment with different values, try changing the y or z coordinates.



There is however, a big problem with moving objects this way. The more frames per second your game has, the faster the objects will move. There are a couple of ways to fix this, but the simplest is to use a different function. Besides Start and Update, Monobehaviour also gives us the FixedUpdate function. FixedUpdate is similar to update, but it is independent of your frames per second. It runs at a fixed rate, unless you game is reeeaaally slow in general, you should put any movement/physics related code into FixedUpdate, not update to prevent weird behaviour differences on differently spec’d computers. Unity also preferes physics calculations in Fixedupdate. So go ahead and copy the Update function, add Fixed in front, and comment out the code in Update. 

You can also change other properties about the transform, like the localScale, or the rotation. LocalScale uses a Vector3 like position does, but rotation is a little different. To calculate rotation, Unity actually uses this thing called a Quaternion. They are very complicated and not really meant for direct human setting though, so instead, you change the rotation through a different variable called eulerAngles. This automatically converts to a quaternion which Unity will use behind the scenes. Not that you can see rotation on a sphere anyway, but you can see it change in the inspector at least.



And that’s pretty much it for changing position using the transform. 
I’ll leave you with some reasons you may want to do this. 

- The transform is simpler and quicker to use, if you need something fast, it’s a good enough reason to use this instead
- It’s more precise than the Physics way.
- If you need very precise movement, transforms are the best choice. 
  It is more lightweight. If you have something that doesn’t really need to interact with the physics system, or that you have a very large amount of (think something like bullets) You can save on some performance by using the transform instead.

Now onto the Rigidbody. Our sphere is lacking in a Rigidbody component, so let’s add one to it. Make sure you don’t select Rigidbody 2D. This should add it to the bottom of the inspector, but I like to have all of Unity’s components at the top, so I’m going to drag it above the PlayerMovement script. This can be finicky, so you can also right click the top of the component and select Move Up or Move Down. Next, uncheck the Use Gravity box, otherwise we’ll just start falling

![img](https://lh5.googleusercontent.com/oq55if_X8ouWdvm3nVcOQ8chFS86efcWT9DJWKcNjRjMc4Zqq3IwZVK3evKVHaKp7NnIVqYAtrMoCS-kkIE0dldrUWYm-9WkmHWzqCNHok_PJ3_nPE75dwbwJxfqbLGZRHAWM_rf0jc)

Now, to use the RigidBody, we need to get a reference to it, which we can’t do like we did the transform. I’ll first show you the easy way, then the correct way, then the more correct way
Let’s create a variable in our PlayerMovement class of type RigidBody. Generally this variable is called `rb`, but `_rigidbody` is also fine.
We’re also going to mark it as **public**. For those of you who don’t know access modifiers, one of the big idea’s of OOP is keeping everything on a need-to-know basis. If there is a variable that should not be referenced/called outside of a class, it should be marked **private,** meaning it can only be referenced inside that class. Public variables can be referenced anywhere. For example, the transform’s position is a public Vector3, this is why you can set it in PlayerMovement.In Unity, public also means it shows up in the inspector, go and take a look.

I think our Rigidbody would be a good fit for this box. You can either drag it in, or press the button at the end and select Sphere there:

![img](https://lh6.googleusercontent.com/O8qrWnRNm9lrqd3Luiu7APBig1MR4BOhRLo7U4dtHMEgGMFqK7l8tkZ-l4g23V_EviV3f3M_-fxIztabqEGgePM2KfaAZwBE8viVuLZDBn5bkSfXOseUq9ndJMyb6mSEZDAAkZYaUCE)

And that’s it, our Rigidbody is now set. But remember, in OOP, we should try to keep things on a need to know basis. Right now nothing needs this Rigidbody, so let’s make it private. Go back to Unity and you’ll see the variable has disappeared…but fear not, for there is another (correct) way to get something to appear in the inspector: ![img](https://lh5.googleusercontent.com/OociJthV2NaTf_ZMsiTdDLzkxxCFUCL0gQXorNzQrgh-WW9U0Uhfc-x_aQ5l0GH8bd6kZ1bJEYkplGt7E4i_WrRyiYTAfEmznVA6t1Co9jLzmbjf0UiQ-weOJMScT0rC4Fo-uZPllSw)

Go back to visual studio and put this above the Rigidbody variable. You should be able to set the Rigidbody again in the inspector. 

This is an Attribute, Unity has a bunch of these, but let’s just focus on this one, and it’s opposite `[HideInspector]`, which I think is much more appropriately named 
For your convenience, Unity automatically marks public variables as `[SerializeField]`, but you can hide them if you wish with this other attribute. 

This does however have one problem. If we wanted 100 sphere’s to use this script, we’d have to drag the rigidbody in place for all of them, which would suck. There is a use for this method, but we will get to that later.

So the best way to do it is like so. In the start function, we need to get the reference to our Rigidbody. Now, since the Rigidbody is on the same GameObject, this is actually fairly easy. There is a Monobehaviour function called GetComponent that, believe it or not, gets a component. Specifically, it gets a component that is on the current GameObject.

```c#
void Start()
{
  rb = GetComponent<RigidBody>();
}
```

This is a **generic** function, which means it has many (infinite actually) versions that depend on the type you give it. In our case we want it to get a Rigidbody, so we put that type in between the <>.

Now that we have our Rigidbody, we can use it later in our code.

In the FixedUpdate function, let’s add a force like this: `rb.AddForce(1f, 0f, 0f);`.

If you run it, it should move to the left like before, but if you take a look at the Rigidbody, you’ll notice that it’s speeding up:

![img](https://lh5.googleusercontent.com/OBhAPOAuf5HVqKhhs_9IODp7ct-O-XrD07uCSUo4hiAQRy-1cIMOX1Pi_stYiJQtrzT4lIP27i2M6FiNucm0KX0Y5alo5iqgblkI0UcISD_7Odbc6i7m-ME2mHDOh1W7lHiL6stR6hc)

This is because we are continuously adding forces to this object with nothing to counter it. Giving our sphere a drag (basically wind resistance) should counteract this once equilibrium is reached. Play around 'til you find a number you like.

Note: any changes you make while in play mode are not saved. If you want changes to be permanent. Make them while not in play mode.

The AddForce function also has a 4th optional parameter which is an Enum called ForceMode. The default is `ForceMode.Force`. [Unity’s documentation on them, however, is not very clear.](https://docs.unity3d.com/ScriptReference/ForceMode.html
)

![img](https://lh4.googleusercontent.com/uAewl37XG7Rv-ECeFH7OFs_GR0b4A_A2XKmLLELOjCGTkudBa_SugIwX-jR90nHnjzDX61Uw-uU9TczYQ1YvdZwqXxfFgQze_41etdEjXeniSqFjKpwNlVko87K4nR3rzgXBn88_Ddo)

See what I mean> The difference between Force and Acceleration, as well as Impulse and VelocityChange I think are clear. But, what does continuous vs instant mean?

The difference is in how smooth the force is applied. An instant force is applied well, instantly. On that exact FixedUpdate call, all at once. For certain forces that you want to be explosive (like idk, explosions or something), this might be ideal. Continuous forces are applied more gradually, over the course of many fixedUpdate calls. This can result in more realistic forces transfers in situations where force is not immediately transferred. 

The best way to see it is for yourself. Try testing this script with both forcemodes and with a drag of 0.5. For me, the impulse version levels out at a velocity of about 99, while the force version levels out at about 2. With ForceMode.Force, the force is applied gradually. So, the object has less force applied overall, resulting in the lower overall speed.



Here are some links if the difference is still a bit confusing (Overall it’s not that important though, so don’t sweat it too much): 

- https://www.gamedeveloper.com/programming/understanding-forcemode-in-unity3d

- https://www.reddit.com/r/Unity3D/comments/6hbp1a/continuous_vs_instant_forcemode

Instead of drag, we could also move our AddForce call to the start method, which should also make our speed constant. Note these are doing different things, but have similar effects. While having drag will make cause the acceleration to eventually reach zero, only applying the force once will give us a constant velocity from start to finish. Albeit, a much smaller velocity, but a constant one. You can also set the velocity directly if you need that level of control.

```c#
rb.velocity = new Vector3(1, 0, 0);
```

And that’s pretty much it for physics. Obviously there is a lot more to know (we didn’t even touch rotation), but for our purposes this will be plenty sufficient. In the later tutorials, you can customize the movement to be done however you want. Change up the forcemode, set the velocity, or event use the transform if you want. It’s your game, so however you want the movement to feel is how it should feel. I’m going to go with Adding forces with the addForce() method and no 4th parameter (remember that means forcemode.force) but don’t feel locked into that. 