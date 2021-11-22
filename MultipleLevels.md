# Multiple Levels

> You get a level, and you get a level

The last thing we’re going to go over is how to make more levels for your game. Or more specifically, more scenes.

Let’s start with our current scene as a baseline. To make a new one, we could start fresh, but I think it’s easiest to duplicate our current scene and make changes from there.
Somewhere along the line, we made a scenes folder. If you didn’t make one already, I’d do that now. 

![img](https://lh6.googleusercontent.com/YZ1H8geIjurX2_7Pv9NHQfgLpGkLfRqKjcrBaV2lq6AO1ld4jcx9SHELJqunzzQ_uI6qkpfPKFtxHHM-nZRdhFXjoUD7AromhPqoQeFl2IFDGaipxpPAbOhSSNRBo4KgFRq8REVUY0Y)

![img](https://lh5.googleusercontent.com/Wbphm8P6s2IDAAYSI-kW8ZjInwo1PUF3rA0DYnFg_RK0br8SE-8UyyHVXEMGT3FRU8AWiOl7yibcZykQw7c_aN6ujkjg5sqBVF_fLRWp9jzFVYxjA9CZTklZwO0nQrTOb5Fh11VOUUs)

In it, you should see this, which is our scene file. Note that the name matches the name at the top of the hierarchy.

CTRL-D or CMD-D should create duplicate of the scene. Let’s also go ahead and rename them. So we’ll have Level 1 and Level 2, or something like that.
Then go ahead and make them different. Maybe only Level 1 has walls. Or it has more walls. Or less collectables. Or the play area is smaller. You get the idea.
Once you’ve done that, you got multiple levels, now we just need to be able to beat level 1 and get to level 2. 

The first things we need to do is add both our levels to the **build settings**. The build settings are how we want Unity to create the executable for our game. We aren’t doing that right now, but there is one other important thing it does which is to organize our scenes. 

So go to File -> Build settings and you should see this:

![img](https://lh3.googleusercontent.com/bAmk5BpyVK8MHAHjIz6yynPSCuwqQnTtWBHaFjtQ7ce9Bi92hUkz3MDxM91jNLP-UaLda-STxUGvKhTkKUNPIBMJNAVmhq38oWW7SnORIn4RJyqwIIT-kg3zJ75uY7ancVeVO0BfJrw)

Go ahead and drag the scenes from the project view into this box, which should add them. If your Level 1 scene is after your level 2 scene, then you can reorder them by dragging them. 

![img](https://lh4.googleusercontent.com/fZhK7zTV5ac5c4QeIcEjN98l37VpZycQRMTKYOt04Wr2pR9becVPBj_0Cy8eEMnhbMs51mnF9omi_v-us3bEZua88PidKvaHKwlp0jH1iUVeM-t6PFNYHPzvj4d_eugrZTc0TAhujLE)

> Note that this number is the **build index**. This will be important in a bit. 

What we need to do is set our scene to be the next scene after we complete a level. To do this we need to use this function: `ScreenManager.LoadScene()`.

You will need to add `using UnityEngine.ScreenManagement;.

Next, we need to know what scene to load, and to do that, we can use either its name, or its build index. Remembering what I said before, the name is generally not a good idea, so let’s use the build index. The way we have our game working right now is that the levels are in increasing order. I.e. level 1 ins index 0, level 2 is index 1 and so on and so forth. 
So, to know what level we need to load, we just need our current index `+1. 

And we can get that like this: `ScreenManager.GetActiveScene().buildIndex`. 

We could also have our code reload the current level if you lose, but I’ll leave doing that to you. 

If you test this you’ll see that there is a change in the lighting when you load a scene. This is apparently an issue with the Unity editor, and it doesn’t do this when you load the level in the actual build version. 

To fix this we just need to bake in the lighting, which you can like this: 

![img](https://lh4.googleusercontent.com/qvC7_ThpvgCZE2Mq2fbLkGxFUWXhQ6WWeff4uxuLwcxscE7JFj7YdMedyx9ND3bmxYmzHfR6rNwn4-pkl6sbVzIjYqDwRBd99y8IvIMOKRrSZQEc4mmNlqjwgZ616IYgz7g2TOEs7Ms)

![img](https://lh6.googleusercontent.com/tmrsxwif7lShzVbqcH4SIcwVkcP2ifaY8VFHwqZWByju0dt-t6f6R6Pgaq46tnOBAKVK-TBhHszBAFW16VUbFtf3oeygsBxPZbG1ZtGSdqopvqNHUDssI4LibaPGhHseHxq8h5lmyM8)

You need to do it for every scene, unfortunately. 

Now, when we get to the end of our levels, we are going to have a problem, so to fix that you would probably want to have a final win screen that would break the cycle. One more thing is that now our "you win" text doesn’t come up anymore since we instantly load a new scene. So, to fix that, let's wait a few seconds before we do that. 
There are several ways to do this, but the simplest is with the Invoke method. 
To use the invoke method, you need to move the code that changes the acne to a function. Then you can call the function after an amount of seconds with the Invoke method like this: `Invoke(nameof(LoadNextScene), 2f)`.

You could also use a string literal instead of `nameof()`, but this way is better. The second parameter is the number of seconds you want to wait. If you had code that replays the current level if you lost, then you will want to do the same for that one. 
Now, you may be thinking that it is is wasteful to have 2 functions that do pretty much the exact same thing. And you’re right. Unfortunately, Invoke does not allow us to use parameters. So, to do that you’d need to use a different method.

The other 2 ways to do it are with **Coroutines**, or the **async** keyword. But I’m not going to go over those here. Feel free to look them up if you want.

And that’s all we’re going to officially cover - Congrats!  But that doesn’t mean it has to end here.

You can add more features to the game. In fact I encourage you to. You could add enemies, different collectables, doors, power-ups, non-square levels, levels that have multiple floors, sound, and pretty much anything you can think of. But for now, you should have a solid foundation to build off of. Like most things, the best way to get better is to practice. Try making a different game. If you don’t have an idea for one to make yourself, try recreating a retro game. The more you do Unity, the easier it becomes.

