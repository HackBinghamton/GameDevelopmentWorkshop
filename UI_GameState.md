# UI / GameState
> Text, for Pros

When we collect one of our floating cubes, nothing really happens. Sure it disappears, but there's no feedback to the player. There's nothing to let them know that they did a good thing, and that's bad. So let's change that.

The first thing we're oging to do is set up a counter that shows how many collectables are left.

Let's start by getting the UI setup for this, then connect it to some game logic.

Right click the heirarchy and find this text option under UI. 

![img](https://lh3.googleusercontent.com/jFlek0eDiXPTa0g_eUUC_T2oYozs9R9NdhPV0T50QRuNlyFV23ElzkXb_mbakh-Mc_pEo6UWu5fdUR-rKG-cwlqNcAvtOPT-jM7YUItdAjI7BYvmyADC8QKeTBMFVJbLDpVO5bhrLNwB)

You'll find that doing so actually adds 3 GameObjects to your scene. A **Canvas**, a **Text Object**, and an **EventSystem**.

The **Canvas** is where you are going to put all your UI elements. When you create Text Objects and want them to behave like an overlay, you need to put them on a canvas. Otherwise you will just have free floating text in your game, which may be what you want, but in our case, it is not. 

The **Text** object is the GameObject that stores our text. It has components that define *how* the text looks.

The **EventSystem** is what will handle any clicking on buttons and such of other UI elements that you may add. We don't have any right now, but you may add them in later and there are a lot of headaches involved in forgetting to add it back in. So I'd just leave it there.

 ![img](https://lh4.googleusercontent.com/qIF0GEUQuDVJ3gB3EPJpha5HlTCO1DLkZek4jlAWFUxWzo2NjoKcsKfVP8NC7NqgsRsQG8JECEVNKgREqRffFjUPka7WlRrnUPtbXX7RBGmPch2JfTUcxwVtwbCB0rD1fu2k2IYCV5T3)

![img](https://lh3.googleusercontent.com/hd6JlQZfiNj6d9K1yfSO6iedF7uzzS3DYpDeD7WVZ1VkuXj-d90FuWBc2fH_EnGNy6E14g0rH6a6FrAkZFHjKoqcXOiTWvbGxlX5hC-IcAWm8EDloIiruirD9JAZEPb6gJjy0P67Mi9I)

> If you get this popup, just select Import for both.

You may be wondering why we chose TextMeshPro and why we had ot import some assets just to get text. There is another way to get text, it's just called text and it was how you got text in Unity previously. You can still use it, but it's...not good. 

So much so that several years ago, some poeple made a tool for better text in Unity and started selling it. And enough people bought it that Unity ended up purchasing that tool and added it into Unity for free. 

In case you haven't guessed it, that tool is TextMeshPro. Unfortunately, TMP (as the cool kids call it) has not taken over the original Text Objects' place quite yet, as some old projects are probably still stubbornly refusing to upgrade, making both remain. But it's getting there.

What TMP does for us is give us much more detail at large sizes. It's also not really any more difficult to use either, so you might as well use it instead. It's free detail. 

But back to our text. Go ahead and select the text obhect in the heirarchy. Then move your mouse to the scene view and press "f". This stands for "focus" and will jump to whatever GameObject you have selected. And at a mostly appropriate zoom level too. 

Now, where this text is in the canvas is where it will appear on the screen. And that’s why it doesn’t matter that the corner of your canvas appears to be the origin. You see, canvases work differently from normal GameObjects, They don’t actually appear where they are in the scene, you can test this by switching to the game view. 

Mine, for instance, is in the bottom left corner![img](https://lh6.googleusercontent.com/i4CB0BbXR85gNdyLmp5bHz11KKSIjZIWkYmj5GPsfV8Eli33zozguHFuTmwxpaCuBAQY665BSPtwxdsYlhZOpgkIdBZ-pXFfY74HmKWqa5ZlSNNNYLtAM9CR2dc5TzSPUX5EaRerZbLN)

![img](https://lh6.googleusercontent.com/YXlUJ094MStV0CG-goRthlefz2XL23fPvluDVQdd-P94qJuzgEXKkLTCr3dfaOal1ZlcWpEi8kEgPk9_gxazrUdqcd63M-6tynQAVXaxVPf2vFz5EC233VS9B2MuK-RyeJGdCZVnjOr6)

Let’s start by moving our text to the top left corner of the canvas. You can do this by dragging the arrows, or directly on the… transform?

Well, yes but only kinda. This is a special transform that’s used for UI. It works mostly the same, just with some different names. The width and height are kind of like the bounds of a text box. They correspond to that yellow box you see around the text. Anchors has to do with where your text appears at different screen resolutions. You probably shouldn’t mess with it directly, we’ll see it change in a bit.

![img](https://lh6.googleusercontent.com/YyOTryHHA7CQy3DXw6QvhyPM0UiKDO7fDEVQGj-6wXrRyhBOijRV9fLbMQznko6Y7b23vsF729ueo0tfwCaFFIFHQYMXK4BwLEmnYRQzFnDoDwmjnU4druPhI7ZFSZP2aGyfUiU_6fps)

Pivot is where you want the center of movement for the text object to be. `(0.5, 0.5)` indicates the center, `(0,0)` indicates the bottom left corner, and `(1,1)` the top right. You can go above/below these values as well, although the use cases for this are a bit slim. 

Rotation and scale should look familiar. Now, let’s reset the transform. You can do this by right clicking where it says RectTransform and selecting reset. 

![img](https://lh6.googleusercontent.com/aOUz2GfOcFJXXUOgJJjGx9qIRsB8-8NJyLbnrvADMUhgLdPw864-0If7_RipMarInQFV6iaZVGan8XiZ9mvpdEdl5hWV2AiDZHpHcnng7c_z5q05Ja7YNRJexFXLuOUDQn_gA5SkLNGJ)

For this next part I recommend making the inspector window bigger. I dragged it to cover up about half my screen. Then click on this weird looking thing that has probably been weirding you out. 

![img](https://lh5.googleusercontent.com/ww4PfqGhjh4DrGG-NzrcX19JA9R8mNpAKMUPBWDPfc137s5eywBBEQoRnPjUnc4Q6MR5uipvKLcEFhD-qqgDC6lL9Vxmo8_dYbAhkyMz9Klj17bOey_WQ_VEfHYCE51w-0wh75_eEMVk)

That should bring up this funky looking interface. The best way to get a sense for what this does it to just try out a bunch of combinations. Note that you can also hold Shift, and Alt (CMD on mac) or both to get some extra options. In case that doesn’t work, here’s the gist: just clicking will set the anchor point. On its own this won’t do much unless you change the screen aspect ratio. Shift-clicking will set the pivot point on the shape. You can see the origin of the transform change as you do this. 

![img](https://lh4.googleusercontent.com/5j42PY0QJHVDAc1ODry4DxZe3Oh_TxzWjocvadEObeFRNxO_8L2sa0RRaQapH80heIPlEgxR3DJ1mgnoZ4T1OvMKXAzlAGv7-LRi9na7kRHEhHiNSdinCy9X4lMR3pl_lAdIHXWmvO4L)

Alt click will set the position of the transform on the canvas. This also sets the origin point. So if you alt-click at Top x Left the `(0,0)` point will now be at the top left corner. I believe stretch is self explanatory.

Let’s set the anchor and pivot point to the top left. Let's the replace the text with “Blocks Remaining:”. I’d also make it so it only takes up 1 line. You can do this with a combination of increasing the width and decreasing the font size. Font size is in the Text Mesh Pro component. If you want to mess around with the settings on the TMP component feel free to do so. There are some pretty cool effects you can give it. The only change I would definitely make is to change the color so that the text does not blend in with the game board. The setting for that is called Vertex Color. 

Let’s also rename the gameObject to have the the text it has displayed in the name, so something like “BlocksRemainingText”:

Lets then duplicate this gameObject (control/cmd + d when you have it selected).

Then change the text to how many collectables you have in your scene, move it to after the colon in the other text object, and rename it to something sensible. So, there are basically 2 things we have to do throug the hscript. The first is to set this number initially. 

![img](https://lh3.googleusercontent.com/e8z3M63AHaDMeb9uVKMTYa37J6KARq-k98lpwW1YerJQehR2WGRs-bHtWgHLgDvXl9vKP-WqgiDhioo8Mm7j9aax10Ez8_R-RfQY50l-Q2taBL2GP8BeTSMZM3osabb29MT1QA4SzfnU)

Now, while we technically have the correct number here, we don’t want to have to change it every time we add another collectable. We also want this to work on any level we put it in, not just this one currently. So, we need a way to determine how many collectables there are at the start of the game. Create a new script and put it on this (the one that has the number) text object, and call it score or something like that.



Since this is a change that need to happen at the start of the game, start seems like a good place to put it.

If you look at your CameraMovement script and how we got the reference to the player, we are essentially going to do that. I mentioned when we made that script that there is another function that gets ALL the references to a certain script. And that function is `FindObjectsOfType<PlayerMovement>()`. So we just need to look instead for our Collectable script. Store the result of this in a array of Collectable classes like this:

```c#
Collectable collectables = FindObjectsOfType<Collectable>();
```



You can then get the length of this array with `collectables.length;`.

What we need to do now is set the text of this GameObjects TMP component to this integer. 

You can use the getComponent method to get the TMP component.

```c#
TextMeshProUGUI text = GetComponent<TextMeshProUGUI>();
```

This will cause an error though since TextMeshProUGUI (don’t ask why it’s so long) is in its own namespace that we need to include explicitly. Visual Studio may do this for you if you hover over the red text and select Show Potential Fixes. Or you can just type `using TMPro;`  up at the top. 

![img](https://lh4.googleusercontent.com/2BnJoRKd06ZCggU6d09vdGjyx8h1bNKtMLs4661215miyKYBCuJxegYZf3E5iesZqxQgyhxJAnUkRRTffr5FwzffIVpZrgTneuWIzyE6K6aCU7puHTmQ55cVcYjzB5KLXPY_1u03MxLu)

![img](https://lh3.googleusercontent.com/JXffwjnTXfZNn6UMaYk74eW_OsrtL_4tuNb1EuQyAIOaV5uLv-g297Nlvi9RHbNxmdu1OMzY2OaQNWjwr9MG-ClYskLhBRLf3wsmvK3hdfMQQQjGQFcVSE1IbKOBIVcA2SW_IqrU1va_)

You can then select either the first or second option. The first is probably better though.

And now we can set the text to the number of collectables in our scene. We do have to make sure to convert the int to a string before hand though. 

```c#
text.text = collectables.Length.toString();
```

And now it should work. To test it out, go ahead and change the initial value of the text to `0`. You should see it change to the number of collectables you have when you press play. 

Let’s delete the Update method on this script as well. We won’t be using it and Unity can actually optimize it out if you don’t explicitly call it. This goes for any method you get from `MonoBehaviour` as well. So if you are not using a start method or you end up deleting all the code in an `OnCollision` method, make sure to delete the actual function call. It’s a small optimization but an optimization nonetheless.

Next up is reducing this number by `1` every time we collide with a collectable. Now we could just continuously check the number of collectables in our scene in an update method, but that is extremely inefficient and wasteful. Instead, we can just reduce the value of the text by `1` every time we detect the collision between the player and the collectable. 

Let’s start by making the logic reduce the value by `1` in this script, then worry about calling it from the collectable script. We’ll need 2 things. `1` is an int to store the number of collectables remaining and perform arithmetic on, and the other is a public function that reduces both that int, and the int in the text by 1. You have all the tools you need to do this, so I would try to do this on your own first. The next slide will contain a more guided approach if you get stuck.
Hint: the local text variable should probably become a class variable that is set in start



Create the integer above the start function `private int numCollectables`.

Let’s also make the text variable a class variable: `private TextMeshProUGUI text;`.

And set both in the start method:

```c#
numCollectables = collectables.length;
text = GetComponent<TextMeshProUGUI>();
```

Next, we need a function to lower the score:

```c#
public void CollectCube() {
  numCollectables--;
  text.text = numCollectables.ToString();
}
```

Ok, now we just need to call this function anytime we collide with a collectable. So in our Collectable script, we need to add 2 things:

- 1 is a reference to the Score script.
- A call to this function. 

Again, try this on your own first.

Declare the score variable:

```c#
private Score score;

// Start is called before the first frame update
void Start() 
{
  // Initialize the score variable to be the score object
  score = FindObjectOfType<Score>();
}
```

In the collision function, call the score method:

![img](https://lh4.googleusercontent.com/rGZfp3-CqW7N2snT92T8XgdS3dp5QLDBONC8b7fQsNvtidcdyXXVwc4Gy-NuSLuv_Vpc5041tVLfdQsGnh6tVchOlMUvf4V-f0WetuJkR5p17VKWfHavJPzDVO2AbkDsAZqr5kXKYeVx)

And now we should be able to see the score number go down whenever you collide with a collectable. The only problem now is that nothing happens when it reaches `0`.
So, we need to reach some kind of game over state whenever that happens.
Let’s create a Game Manager script to handle all this. Note, if you call it GameManager, Unity will make it look like a gear. It doesn’t do anything special, It’s just neat. 

![img](https://lh5.googleusercontent.com/3vWEHcIv7KHFTxo6tn9aXRGFkqJwnEdBUuRzcVOCCKnMvDHrGhWNpBAI8VX1nAKZWHqMvYjVnxMMglfONuCFR0eM6RjdgiNYbYt2XAjuVnrfzlGwDqB7cXdprUzvuxzhz3OoTc3gTD4)

In this, we’re going to make a win function and a lose function. We don’t need to put anything in them yet, lets just have them.
Next, let’s create another Text object (duplicating the old one is probably easiest but you can make it from scratch if you want) on our canvas called GameOverText. We can just put the words game over in it for now. Let’s also put it in the center of the screen. Remember, you can do this by setting the pivot point and position by clicking the graphic an selecting the middle one. Let’s also make the text a bit bigger and center justify it. You may need to increase the width so that it doesn’t wrap the text. You also might have to adjust the bounds of the yellow box to make it centered.



Once you’ve got it to a place you like it, let’s turn it off. Click the check box next to the GameObject. This will deactivate the GameObject. You should see it grayed out in the hierarchy.

![img](https://lh4.googleusercontent.com/yY7mqkoDcQqLuEHCr4U09nfcnHGJ2N_L_wSRIT3_wwj-VlB8jwyf6C2pEHsDNIZIBf8hSVQgs4GQHfsdRdLgjf0JX20WlRKIuyfsGHvqcDIZJgW_lrG9tKb2GKfURA_NB_qaoP4grOQ)

Now all we need to do is set the text to either a win message or a lose message when you win or lose the game.
We currently don’t have a way to lose the game so let’s do the win one first.

In our GameManager Script, let's set this text to say something like “You Win!”

For this next part, we’re going to need a reference to the text component. Now, that’s a little hard to get through code seeing as there are 3 other text objects on the canvas. `FindObjectsOfType<T>()` would require a little more work. The simplest way would be to do it would be to make the text variable serializable in the inspector and then drag it in. However, if you are doing this that usually is a hint that something should be changed. In this case, it would probably make sense to make the whole thing a prefab first (wait don’t do it yet). That way if we make other levels, we can just drag this prefab into the scene and not have to worry about setting the reference. In general, if you are going to set a variable through the inspector, you want it to be in a prefab. It’s not always going fit to be a prefab, and sometimes you just need something quick and dirty, but in general keep this in mind. 

Create an empty GameObject called GameManager and put your GameManager script on it. Then drag the canvas and EventSystem under it. Now drag it to the Project Window to make it a prefab. Now double click to open the prefab. When you drag the text object in, make sure you are doing it on the whole prefab, not just the instance of the prefab that is in the scene. They are different. And at this point I’m just going to say make the text variable, assign it in the inspector, and set it to your win message in the Win function. You also need to set the `gameObject` to active, which you do like this: `GameOverText.gameObject.setActive(true);`.

Similarly you should do the same for the lose function. If you are having trouble, look earlier in this section for the full process.

One thing you may also want to do is refactor our scoring code to now go through the GameManager. You can even get rid of the Score script entirely and move all its functionality to the gameManager script. The game will still work the way we have it now, so this change is optional. It would just be more internally consistent and simpler if we refactored it. If you do delete the Score script, make sure you remove it from the gameObject **in the prefab AND the instance of the prefab in the scene**, otherwise it sorta kinda sticks around a little.
Oftentimes you will come across situations like this. You make a change and suddenly the way you did something before now no longer makes the most sense. Whether or not you refactor it, of course, up to you. Just remember, even on projects where you are the only programmer, you can still write code that is hard to read and harder to debug.

Next we actually need to call our wind function when we, you know, win. So, in our score function (either in the GameManager or the Score script), we just need to check each time if our score is `0`. (make sure to do this after you subtract). Then we just need to call the win function. If you have the score function in the GameManager, this is easy, if it is in the Score script, you will have to first get a reference to the GameManager script. Also, based on which you did, the Win function should either be private or public

Next is the Lose function.

How do we determine if we lost? Well, if you don’t have any walls, then falling off the platform is a good indication. If you do have walls, you could either remove 1 or more walls, or make it so you can only hit the walls a certain number of times. You have all the tools you need to do the second option except for 1: how to know if you collided with a Wall. It has no scripts on it, so the only thing we could do is check the name, but this is slightly unsafe, as the name of a GameObject is super easy to change accidentally. Say you wanted to start describing what the wall was, like putting north/south/east/west in front of it. The point is, you generally don’t want to rely on the name of a GameObject.

So how do we get around this? Well, Unity has these things called tags that are useful for this. Each GameObject has the option to have 1 tag, by default they have the tag “Untagged”.

![img](https://lh3.googleusercontent.com/4LIdWFaj25vq1MXYG5cyQduaYOPhBpfgQLyJu-eVlesBzxK9BadsgVCqG6khaCfRqh71Jqx8gfboKTiMnuImVo2EJ4jxyVbut44IwCuln2xSl5ybs1KoAQFSVTebjHShqZG9S1R93lM)

So, to add a tag, click this button and the Add tag option at the bottom of the context menu that appears. Then you should see this:

![img](https://lh6.googleusercontent.com/UdgUhv5IUZfg-MIcgJ3DWLgSlyybEERrb5xfOi3a_PAl2ocOv42HSAQUUuS4X2omV6QoJZV9o1YStxHlRqGe6E7whDJZ6UDi1LoZ0PsZGZRNPNKTWsqj9AwyFFwxwUuRUQOlGjqBjxI)

Click the plus sign and add a new tag for the walls. Afterwards, you will still have to assign the tag to the gameObject. I don’t know why, but for some reason this process only creates the tag, but does not assign it to the GameObject you were doing it to. Then, when you are checking for collisions, you can use the compareTag function to see if the object you collided with has the tag you are looking for

![img](https://lh6.googleusercontent.com/foa879GQAUhAy53YFxfmlb76Ms2yhFDtmDH0RR_udJyVlmpgXOqDO4lMfjJzZCYE4t1f-MQxN__BuYXGGbXhaQpco0Ji-6LZyPP_bVj4SG-qlKTYHHI68Mg_bwDjvHA9UGnmyBKyJDw)

You could also check tag directly with gameObject.tag, but this method is more efficient. 

Now, if you didn’t do that and want to know how to tell if the player fell of the edge, there are a few options. You could check the y value of the player. If it goes below 0, it has fallen off the edge. This works fine. The only thing is that you may decide later that you want to make a level with multiple platforms, and one might be below the other. So this would not work then. You could make it lower in that case, but that is also hard to remember to do. Another option would be to make a large collider below the game area that is a trigger. Then whenever you collide with it, you lose. The only thing with this is that if you are going fast enough that you don’t hit the collider, you have a bug. Ultimately, this is up to you. Whichever you think makes the most sense to you and you think is the easiest to maintain is what you should do. You could even do both. You may even have a completely different way to determine if you lose or not. And that’s fine too. 



Another thing you could do is disable player input if they lose, The simplest way to do this is to disable the PlayerMovement script: `FindObjectOfType<PlayerMovement>().enabled = false`;



If you wanted to have a dedicated lose screen you could do that too, and one way to do that is to have a dedicated scene for the game over screen. You could also have a separate canvas in this scene, then turn off everything in the scene when you lose and turn on the lose canvas, but that seems like a lot of work. It also won't scale as well if you have multiple levels since you’ll need to make it for each scene. Conveniently, the next lesson is about making new scenes. 