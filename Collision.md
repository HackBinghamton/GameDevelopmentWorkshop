# Collision

> "Bonk"			- Not Bethesda

Now I think it’s time we added some other entities to our game. Specifically, some collectables for our player to pick up. To do this, let’s start by creating another cube gameObject in our scene. Remember it’s right click -> 3D Objects -> Cube in the hierarchy. 

Set the position to 0,0.5,0 so it’s on the ground plane. Then feel free to move it around using the move tool so it’s not directly on top of the player, but is still on top of the plane. 	

​					 				  ![Untitled](/Users/ronlaniado/Downloads/Untitled.png)

Let’s also make it a little smaller and rotate it on it’s corner. Change all 3 scale values to .5 and 45 degrees for the rotation on all 3 axis.
If you still want to move it, you’ll find that’s a bit harder now that it’s rotated. The arrows are pointing in all weird directions. This is because the scene view is using the **Local** version of up/down, left/right, and forward/backward. To change this to the **Global** version, you can click this button above. 

- *Local* means that you are taking into account the orientation and state of the object you are looking at.
- *Global* ignores all that and uses predefined version for all 3. You may also see **World** as a similar name to this.

It’s important to keep this distinction in mind when programming. For example, our addforce call to move the player; in this, we give a Vector3 in world coordinates, or a global Vector3. This means that no matter how our sphere is rotated, we get the same direction. In our case this is what we want, but if you want the local Vector3, then there is a different function, `AddRelativeForce()` that you should use instead.

I recommend switching it back to local after you are done. 

Now our collectable is also a bit hard to see on the plane, so let’s create another material with a different color and give that to our collectable. If you don’t remember how to do this, it's in the middle of the Input/Camera tutorial. 
Let’s also make a script for the collectable to use. I just called mine Collectable. In fact, let’s rename our cube to Collectable as well. Make sure your collectable script is on the collectable and in the scripts folder. Depending on how you made it, one of these will need to be done.

First of all, we’re going to make the collectable move a bit. If you made your character move just using the Rigidbody, which I’m assuming most of you did, this is how you can do it with the transform. 
In our update method, we are going to use a function that the transform has called Rotate. 

```c#
transform.Rotate(new Vector(45f, 45f, 45f));
```

In it you give a Vector3 that contains the degrees you want to rotate the gameObject by. Now, remember that Update is called every time the frame is redrawn. 45 degrees every frame is a lot. Also, recall that update is called a variable number of times a second. Different computers will run it differently, and also as our game adds more entities, it will also slow down.

So how do we fix this?

Now, we could put it in FixedUpdate. That’s locked so it would always be the same. But that’s not a perfect solution. Since our screen is redrawing more often than FixedUpdate is being called, our collectable is not moving for every frame update. If we want the movement to be as smooth as possible, it should be in Update.
So, to get around this, we need to use some math (yay!). Luckily, Unity provides the hard part for us. Essentially what we need to do is multiply the amount we are changing the rotation by a value that scales inversely proportional to the frame rate.
Or, we need a value that gets smaller as the frame rate gets bigger. 

And like I said, Unity provides the hard part. They have a static variable that you can use that contains just such a value. This is the amount of time that has passed since the last time that update was called. So, the more times update is called per second, the smaller this value gets. 
So, in order to get our rotation to be constant, you just multiply the Vector3 you made by this value. Multiplication of a Vector3 and a float just multiplies each value by the float.

Feel free to pick other values to rotate by, remember they are in degrees. The way the math works out I believe it will end up as degrees/second. 

There is also a function to do this movement for the position. And that is `transform.translate(new Vector3(0f, 0f, 0f))` (not this is the amount you are adding to the current position, not the new position).

Now onto the actual collectable part. If you run into the collectable right now you’ll see that you just bounce off of it. This is because you both have a Collider component (remove it and you’ll go right through it, try it in play mode). 
This is also why you are not falling through the ground we created earlier. Unity has built-in collision detection of objects, so all you need to do is add a collider. It also lets you run code whenever collision occur.

There are 2 functions that do this:

```c#
private void OnCollisionEnter(Collision collision) 
{
  
}
```

```c#
private void OnTriggerEnter(Collision other) 
{
  
}
```



They do essentially the same thing, the only difference is the type of collider they are called on. They also have different parameters, the main difference being the Collision class has info about the point of collision and stuff like that. But for our purposes, it doesn’t really matter.

The first one is for normal collider, these are the ones we have on our gameobjects right now. The second is for triggers, which are special colliders that can detect when you hit them, but don’t cause the object to bounce off the collision. To make a collider a trigger, there is check box on the component. 

![img](https://lh6.googleusercontent.com/mZRRHo2YwZ64yOTKc3V0XAFzrKAhPOxMpj1kAt31RP4SG03pv8btFFdOyU4Zv6gNgCTPTDUyuPPJjZrT7CJJ0kFQKOYI4NUW4DdelDJfizj57Y2qcpEzMMUYyLhbYp4KBA6_MqlZVGU)

Now, when you pick up coins in mario or rings in sonic, you don’t bounce off them, so lets make our collectable a trigger.

The `OnTriggerEnter()` and `OnCollisionEnter()` can be in either gameObject, so it’s best to put it in whichever one makes the most sense to hold the logic of what happens when the two objects collide. 
In our case, I think it makes sense to have the code in the Collectable class, since the player is likely to collide with things more often that will not be collectables. And it is wasteful to call it if we don’t want to use it. 

On that note, the first thing we should do is check that our collision is with the correct object. Luckily, the parameter to this function will do just that. The parameter to this function is the collider component of the gameobject that we just collided with. So, we just need to determine whether this collider is attached to the player object. 

One solution would be to check for the PlayerMovement script. Our Player GameObject should be the only GameObject to have this script, and it should always have it.

Remember the `GetComponent<T>()` function? One feature of it is that it returns null if the component is not found. So we just need to check if `other.GetComponent<PlayerMovement>()` is not equal to null. And if it isn’t, we know it’s the player.

For now, let's just print out something every time this happens, then test to make sure that it works. 

The next thing that we need to have happen is the collectable needs to disappear after we hit it. 

There are a couple of ways to make it disappear. Here they are in order of severity: 

- Disable the mesh renderer to make the object invisible
  - `GetComponent<MeshRenderer>().enabled= false;`
- Make the object inactive. This keeps the object around, but makes it so it doesn’t interact with other objects or Unity’s systems, like the physics system. It will also disable all the scripts that are on it. 
  - `gameObject.SetActive(false);`
- Destory the object
  - `Destroy(gameObject);`

Since we don’t need the collectable after we collect it, the 3rd option is the one we want.

Now, if we wanted to create another collectable, and we do, repeating all the steps we just did would be very tedious. So, Unity has a built in feature called a prefab that lets us copy GameObjects and stamp them in the scene (and other scenes too!). 
To make a prefab, all you have to do is drag the object from the hierarchy into the project window, which should look something like this after you do it:

![img](https://lh6.googleusercontent.com/ZRaJxVQidD_sl7ZdcUNBE1olFuKFdB8NUPB2r6drp_4RyDbRgksq5Be8TXOXTPbag65YS8X3GakfH2aX39csYv7bMan0bBDBXrDa6US5Xoc89-50Bitf3flBeyO-UKz2Ph-MqA17URc)

And that’s it, this object is now a prefab. To place it in the scene, you now just drag it from the project window into the scene view where you want it to go. Go ahead and add several of these to the scene. Make sure they all have a y value of .5 though, since it’s likely they won’t after you drag them in. To do them all at once, just select them all in the Hierarchy and edit the transform in the inspector. 

Just as a bit of housekeeping, let’s create a new folder in the project view for our prefab called prefabs And on that note, let’s also make a folder in the Hierarchy. Well, not really a folder, but essentially the same thing. To organize the Hierarchy, you can create empty GameObjects and **parent** the objects you want in it underneath it. Let’s create a empty gameObject called Collectables and drag all the collectables underneath it. 
You can do this one by one or all at once by ctr-clickingall of them and then dragging.

![img](https://lh6.googleusercontent.com/z0iAbR7JXE35ZdILA5s3DFmCWOunh4nzutCiefPrSWMWkhCvVdV_sciXNEOO_5MMrNkS-8gLdHhMUBl4VGY9L_gwx8Fsel-dkbtwCu9Fso0LC_X_b9xrVFUprn59aKu23f45onXZZOY)

This makes all of our collectables **child** objects of the Collectables object. Besides letting up collapse the **parent**  object like a folder, this also changes the definition of the position.

If you try to set the position of a collectable to 0,0,0 you’ll notice it goes to some random location on the screen, not the origin. This is where the Collectables gameObject is, which you can verify by selecting it. 
So, now the position is relative to the parent object. This is also called Local Position, which is now different from its global position, which is in world space. 

If you want it back to the origin, the you can move the parent object to 0,0,0. However, if you do you’ll notice that all the other gameobjects move too. Another property of having a child object is that its transform will follow the parents transform. This is extremely useful for 3D models, where the model is comprised of many GameObjects that are all parented, either directly or indirectly, to one main parent gameobject. 
To not have this happen, you’ll need to unparent the children, then move the parent, then reparent the children. 

Another useful feature of parenting objects is it makes them easier to find. All of the objects that are parented under a GameObject are stored in its transform. You can loop through the children in the transform with either with a normal for loop or enhanced for loop a like this:

```c#
for (int i = 0; i < transform.childCount; i++) 
{
	print(transform.GetChild(i));  
}

foreach(Transform child in transform) 
{
  print(child);
}
```

You can also get the reverse, i.e, you can get the parent. To do this you use `transform.parent`.

You can also chain these together to get the parent of a parent or child of a child, although having your code be rigidly reliant on really strict hierarchies is not advised. 

The only other thing I’d like to mention is the idea of multiple colliders. You can have more than 1 collider on a single GameObject. The only catch is that they have to be of different types. i.e. a sphere collider and a box collider. If you want to have more than one collider of the same type, you will need to make a child object and put it on that. 

Try to think about how you might create the collider for a hand. As well as how detailed you want it to be. Does each figure have its own collider? Each joint on that finger? Or is one box that covers the whole things good enough?

As you might guess, it depends on the level of detail in your game. But this could more broadly apply to an arm and a leg as well.

I’m not going to go over it explicitly here, but you can add walls to your game board. I’d suggest using cubes that you elongate to cover the edges, although 4 planes that you rotate would work as well. 
I’d also recommend that you make a parent “Walls” object to store them all under. Or maybe a “level” object that includes the ground, your preference. 