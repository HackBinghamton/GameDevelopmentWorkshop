# Best Practices, Neat Tricks, and Extra Resources

> I have run out of funny subheaders

This last part goes over some ways to make your Unity Code work as well as possible, both in terms of organization and efficiency. So, in no particular order, here are some good practices, neat tricks, and extra resources.


## "Awake" Monobehavior

There is another method that Monobehaviour gives us called Awake and it is super useful. Awake is very similar to start, but you are guaranteed that all calls to Awake will occur before the first call to start. 

There is a reason to use one over the other. In general, you should actually be using Awake, not Start. The way you should split them up is that in Awake, you should try to set up all the dependencies that you can. If script A has a reference to script B, then set it. But if script A needs a reference to something in script B that gets set in the Awake method, (like another component or variable) then we have a problem. The order that the start and awake functions are called is random. So we have no guarantee that script B’s Awake method will happen first. So the reference may not exist yet. 

The solution is to use the Awake method to get the initial reference. In other words, have script A get the reference to script B. Then, in Script A’s Start method, get the reference to the component/variable in Script B. 


The other main difference has to do with the object being disabled.

Scripts that are on initially inactive GameObjects will call their Awake and Start Method only when the GameObjects are set to active.

Scripts that are disabled will call their Awake method when the game starts. But they only call their Start Method when they are enabled. Keep this in mind, as it could break something.

There is actually another method called `OnEnable()` that gets called whenever you enable a component. It is similar to how start will work, but will be called every time you enable the script, whereas Start is only called the first time. 

Here is a link to some more reading on Start vs Awake: https://gamedevbeginner.com/start-vs-awake-in-unity/
You can also look at this diagram on Unity’s call order https://docs.unity3d.com/Manual/ExecutionOrder.html#UpdateOrder


## Naming Conventions

These are not hard rules, but generally speaking, it's good to try and follow conventions within a language or industry.

Class variables and components should start with and underscore. For example: `private int _score;` or `private GameManager _gameManager;`

How much you do this or if you do it at all is up to you.

The reason for doing this is that it makes it easier to determine what is and isn't a variable. You know what is a local variable and what is a class variable. 


## Collaboration Tip

Most people are probably going to be working on personal projects by themselves for a little while when it comes to game dev in Unity. And that’s perfectly fine. But, chances are that if you are serious about game dev, you’re gonna end up on a team at some point.

So, this might save you a few headaches in the future. The easiest way to do teamwork in Unity is with the built in collaborate feature. Unfortunately, this is a Unity Pro feature only. So if you (or anyone on your team) have the free version, you will not have access to this.

For those of us who don't, the solution is prefabs. One of the biggest hassles with collaborative Unity projects is editing scenes. They are essentially really big files with all the info about the scene. Unfortunately, this file is not very human reader friendly. So any merge conflicts you get on it are relatively hard to resolve. 

So what you should do is have most of the objects in your scene be in a prefab. Then when you need to edit something, you can edit the prefab it’s located in. If you edit the prefab, and not the scene, the scene does not actually get changed, the prefab does. So, the changes are more segmented and less likely to cause merge conflicts.


## Properties

This is a C# thing, not a Unity thing, and is something to keep in mind when looking at how to do things in Unity. It’s not a huge distinction, but it can help how you search for info/help on a certain topic.

Properties are like condensed getter and setter methods. They look sort of like a variable, and sort of like a function. There are a bunch of ways to write Properties, but we're not going to go over that here. (There are many great websites with explanations if you are curious.)

The reason to use properties is mainly as getter and setter functions. Having a private variable that is in the class and public properties that reference that variable is much cleaner and shorter to write than a getter and setter method.

Properties also don’t have to be attached to variables, they can be functions that calculate values and return them as well. 


## Additional Resources

Brackeys: https://www.youtube.com/c/Brackeys
Lots of good basic tutorials. Easy to follow. Touches a lot of Unity’s system’s and UI. Usually less code focused and more Unity Focused. Hosts game Jams. Sadly no longer posting, but his old videos are still very good.

IHeartGameDev: https://www.youtube.com/c/iHeartGameDev
Really good in depth tutorials on certain features. Relatively new, but his tutorials are really well done.

Code Monkey: https://www.youtube.com/c/CodeMonkeyUnity
More code focused tutorials that go into some of the more intermediate and advanced things you can do in Unity/C#. 

Game Maker’s Toolkit: https://www.youtube.com/c/MarkBrownGMT
Really good videos on game design, currently doing a series on making a game

Infallible Code: https://www.youtube.com/user/charlesamat
Good tutorials about code organization and best practices for game dev

Jason Weimann: https://www.youtube.com/c/Unity3dCollege
Good tutorials on more advanced Unity features and C# coding

Dani: https://www.youtube.com/c/DaniDev
Game dev who makes really good/ funny games and videos

TaroDev: https://www.youtube.com/c/Tarodev
SamYam: https://www.youtube.com/c/samyam/featured

A lot of these youtube also have discord servers where you can ask questions and talk to other game developers.

Unity also has a discord server. Unity also has online forums.

And, as always, Stack Overflow

We also have a GameDev channel in the HackBU discord server!
