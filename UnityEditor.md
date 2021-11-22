# The Unity Editor / Interface

> "Oh god what do all these buttons do" 
> 	~You, probably

Let’s start By creating our new Unity project. Open up the Unity Hub, make sure you are in the projects tab on the left, then press New to create the project: 

![img](https://lh3.googleusercontent.com/dAg1149x3M_F5CbDIz0KBKodUK2LWr8OXC4ngoZ-I5HjMsUQFuuS_sURdmCC-EDR73MymxqDbe5vxRaP53wN6WhxfUCxZdnX3w5oKxRWTZUrcPKBkYjojZJHu1A1lShWWj9PSmZXj30)

Give it a name and location on your drive, then select 3D as the type. Don’t worry too much about the other types, they are for 2D games and professional use.

Opening it up should give you something like this: 

![img](https://lh4.googleusercontent.com/_BkQ601I0xOYD5LuJ6iKSh_UmWAytzAy124uouMsIjw25wpl38dKcQ17s4cTkvkUcUxCqY9g4kZeEd7f9YuGq33fVgQl7GHMiL79Iy8J6k4B_8QTqBb1pDjx6BDMeXsoZ_sQa7UNIRs)

Now this is a lot to take in at once so lets go window by window. If yours is not dark theme and you want it to be, the setting is under Edit -> Preferences.



First is the **Hierarchy**. This stores all the **GameObjects** (more on these later) in your Scene (more on this later too) in one place and shows how they are arranged. For example, In this picture I created an empty GameObject and made it a **Child** object to the Directional Light object. This does several different things, but for now let’s think of it sort of like a folder. Similarly, you can think of the Hierarchy as a file system of sorts for your GameObjects. Feel free to drag them around to rearrange them as you see fit. Just put them back after. 

![img](https://lh3.googleusercontent.com/4EunqgO96kwJoonn6E4FD04Iel4uAMg6NEODv4GYBqIB2eOntKV1EmclkCBZnYvb4FBhoYJSmP05qHu4Rk9gLM6JRW688ftLndeA4NN-gM1D4yNve-65ZHDLdTKRb05p_nXhiaBjVRk)

Now, you should have the main camera and directional light objects in your hierarchy. Unity makes those for you when you create a new project. These are both GameObjects. 

**GameObjects** are containers for pretty much anything and everything in Unity. 3D models, 2D sprites, UI, Particle Effects, Terrain, hell even sound effects are stored in GameObjects. Now, on its own, a GameObject doesn’t do anything. It’s a building block for you to add functionality on top of. To prove this to you, let’s create a completely blank GameObject. You can do this by right clicking in the Hierarchy and selecting “Create Empty”.

You can press the play button at the top of the screen to see…absolutely nothing happen (other than the view on the middle window changing, more on this later). Pressing the play button again will stop the game and return you to how it was before. 

![img](https://lh3.googleusercontent.com/_G9Dl6v87e6AIJ11G0r27m096401RJ17-qdHRSuY5iKtKg374CegyHFkWp4Dc1YyazvMCtgSCcvo2QLLCCLMKRUMiYUtqFp3PUIaXx65WBcX7CpoGkPQLTORYxJd1iQyDaz-cmtOnAc)

To see how to add functionality to our GameObjects, let’s head over to the **Inspector Window** on the right. Select the empty GameObject you just created (in the hierarchy) and this is what you should see. This is the barebones that a GameObject comes with. You got a position, rotation, and scale. These are all stored under the **Transform**, which is the only **Component** that all GameObjects share.

A **Component** is anything that modifies or extends the behaviour of a GameObject. 

Some common components are 

- Rigidbodies (which interact with Unity’s Physics system)
-  Renderers (which display models and sprites)
- AnimatorsCollidersyour own Custom Scripts

You can add Components with the Add Component Button (Imagine that). Go ahead and press it, then start typing in any of the components I listed above, you should see it pop up. You can also right click to remove them after you add them (make sure you click the top part of the component).

To help you get the hang of it, we’re going to be creating a simple sphere that we can use later.

Let’s start by adding some components, namly a **Mesh filter**, a **Mesh Renderer**, and a **Sphere Collider**. Preferably in that order, but it doesn’t affect anything other than the visuals:

![img](https://lh3.googleusercontent.com/2xAvhC3V_Lc1l2P1qTKzkdqhO_MPa82SMjjkwM78JxtGBsmhKF__zQsGHxsxf89IiFj3Jt4htI7xYI3KjB3aKcauG0Kh95lnESSZmAjNT2Fqjq7yRbH6VUFHt4Gbz8DdkNwsPEXEtp0)

Now what are each of these and more importantly, why are there 2 things that say mesh?

- A Mesh Filter is a reference to the shape of the object you are trying to create, in our case a sphere. 
- A Mesh renderer is responsible for drawing (or rendering) that shape to the screen
- I have a feeling you can guess what a sphere collider might do
  - Unity has built in colliders for certain basic shapes, ie, cube, sphere, cone, sprite, etc that you can use on their own or together to create more complex colliders

We only have 2 more steps to create our sphere. First we need to get a reference to a sphere mesh for our mesh filter. Luckily, Unity has one built in and we can use it here. You may notice that our mesh filter currently has a descriptor of none. If you select the circle at the end of the box, a menu will pop up for you to select a mesh. Select the sphere mesh:

![img](https://lh4.googleusercontent.com/qu81CWmHxzvj0y0rHxU1kMrF76_BFIIhF8-OlhoraFJyx8zehKLvKJAQ8Q6a9m6WMXSRJI7oyZa2CWf6Jaa73D0H3LiTm6hMT2dzAZbfHkMc00OU4PqKAmAu5bLWLlrh1KTVy8_LqWo)

Congrats, you should now have an ugly pink circle in the center window of your screen. Unity uses this pink color to indicate that a renderer does not have a **Material**. Materials, along with **Shaders** are what define how a rendered mesh looks. So things like color, texture, metallicness (totally real word btw), glow etc. Let’s not worry too much about these though, they are more the art side of Unity and not really part of this tutorial.

So let’s fix that color problem. Click this arrow to expand the materials list (you can have more than one) and add a new material. You do it the same way you selected the mesh. The material you want to add is called “Default-Material” and you can type that in just like add component button:

![img](https://lh6.googleusercontent.com/6Ap2xW5I-To9jAn2LLYYLGhfy87C-xMdAih0da41JdiJWEfd2ewVMMW4AQjYui2-XdMKiMdIk83hdFuL7OTgnMhuOxYEL-WxpJNes--Vo8IRWk23l5z3SIZvPtgtDKCOvnb-obfORSg)

And with that you have made a sphere. If you want you can rename the GameObject to Sphere at the top of the inspector window. When you’ve done that, your Sphere should look like this 

![img](https://lh3.googleusercontent.com/hGKWrPr17VCq8_odHrMA_9sEDOJbYEjeX3DekOJOACtoX_DUux8P9k9m03mpIKbuI2F68i8puXw07baH8mQ0G6UDf_rumpkuhE3vTXR0CciqEgvMFhQILJBe3bx4cshroLb0hzv-uhY)

That was a fair amount of work to get just a sphere, so luckily, Unity has a shortcut for basic shapes like spheres. In the hierarchy, you can right click -> 3D Objects -> Sphere. This should make the same GameObject we just did, and you can switch between them to verify. And that’s why you should’ve added the components in that order. If you didn’t, you can rearrange them. Dragging is a bit jank, so if that is being annoying, you can right click them and select move up and move down instead. 

Alright, now let’s take a look at the last few windows. The center one I’ve referenced a few times is the **Scene View**. This also shows all the GameObjects, kind of like the hierarchy, and you can select them in there too. 

![img](https://lh3.googleusercontent.com/vZRc4iGQuDyjXEO3YHSr0AVJJ-gP2oMQiWdX2mp8-eEsIHhbwa-F6-qTf0JPf8KNToxsiRI9MEwYzkwaQueDIt39PwlPkJKsHNVgWrfuWWQ6dHud2g_suF0PIGGsho0ElISN_XDw_lI)

As you can see, the sphere we created is in this window. The main function of this window is to show you what the game looks like. Additionally, you can edit the transform component here as well. 
The way you do that is with these tools here:

![img](https://lh6.googleusercontent.com/EMuKUtTz3nNGiZDfJf0nI8MGe8NLyNIC2oCDSrVmqWL5Ezt404GXeGqzDJjKKJTW6alq5C9KArnw0eW6MA0NEPYqgo1KVhAfY5azGaPFZG8WeO0Wb1Rsl4xrxu510GvzyjKiLZTyMfY)

The first tool lets you move around by left clicking. The second one lets you move a GameObject. The third one is rotation, the fourth is scaling, the fifth is for moving 2D objects and UI, the sixth is all of those at once, and the last is special tools depending on the components you have. 
I find it’s best to keep it on the second tool and switch to the others as needed (which isn’t often). Additionally, you can always move around by using the middle mouse button. You can also always pan the view by holding right click.

Take some time to get used to moving around in Unity. Also try moving the sphere around and changing some of its properties with the different tools. Be sure to ctrl-z it back to the original position before you continue. A tip on the the second tool: you can move the object in a single direction by dragging the arrows, but you can also move it in a plane, or along 2 axis by using these squares in between the arrows: 

![img](https://lh3.googleusercontent.com/vZRc4iGQuDyjXEO3YHSr0AVJJ-gP2oMQiWdX2mp8-eEsIHhbwa-F6-qTf0JPf8KNToxsiRI9MEwYzkwaQueDIt39PwlPkJKsHNVgWrfuWWQ6dHud2g_suF0PIGGsho0ElISN_XDw_lI)

The **Game View** is the window that shows what the game looks like when you play it. In fact, when you hit play, the scene will actually switch to the game view

![img](https://lh4.googleusercontent.com/WDNJImWHsWb-F7Xl7zIJhyAuo9YgSL6crnXH1zxgNJyHQBKTN3-t1pUHG9exi6wWhH-QZHFIRlo0YSVHl6NR46UrtPYlG5SJ72YtWqCNawZXzxSjY9mFcFgDrdhVvIspwWSmPZwF0Lc)

The last 2 windows are the **Project Window** and the **Console Window**.

The project window is where all the **Assets** in you project are stored. Assets are your scripts, 3D models, sound effects, **Scenes**, etc. Scenes are like levels in a game. They’re small sections of a game that you load in at one time.

![img](https://lh5.googleusercontent.com/7bb35o-O50ve3_dos7RMgOSsLbUnufUSf5n8f4xo4a1eF-O9GafCeBWMgcggfr6FCufE55Vym-ifxeLVHlgZEtHJgcGH6P52Oj0uTDyMDkxSCJtaonfO9EYuf71c7EaBKiQnR5mV0fo)

This may be a bit confusing as for how the project view is different from the scene view. But think of it like this: the Scene View shows you everything that’s in 1 scene, whereas the project view has all the assets in your whole game.

And finally, the **Console** is where all your debug messages are displayed. It will also have your warnings and errors as well. I recommend making sure this collapse button is pressed. It groups any debug/error messages that are exactly the same. This makes it easier to look through. 

![img](https://lh3.googleusercontent.com/TlT6W7C6brcy0NyjxgnFX68onznBmoFZ-4xk5u0KrFu1Yqyhp0gWZ-_rphs5wkFCMPh2XD5my6i2Lk0Vn3A2bk4sPzSPG_ZM9wsbZVJ_3EpJ6IPeieDfT26kyJigSh4WhJ0TdnDJvpM)

And that’s pretty much it for the Unity Interface. There are more windows that you can use. They’re found up at the top under the window button, but we won’t be using them for this tutorial. One more thing though, all of these windows are draggable, so if you don’t like the way they look you can feel free to move them around. And if you mess up and want to go back to the old layout, you can select the default layout option in the layouts submenu of this context menu. I’m going to be using the default layout though, so keep that in mind. 

]![img](https://lh3.googleusercontent.com/o4zWdkOA3a1ySaa5dzZAe_RvM3mNShMpgpEyzcPiEJgzcH336WsZgnTbZkTzqM1hyyRGVUzxLSXDpm8eycMFQSxXtPf5GjQ082kC6GzQhsSrr5k5LNJ6ggCujc2ZnBYw0Obw2H5taJk)