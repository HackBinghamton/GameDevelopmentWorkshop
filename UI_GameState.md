# UI / GameState
> Text, for Pros

When we collect one of our floating cubes, nothing really happens. Sure it disappears, but there's no feedback to the player. There's nothing to let them know that they did a good thing, and that's bad. So let's change that.

The first thing we're oging to do is set up a counter that shows how many collectables are left.

Let's start by getting the UI setup for this, then connect it to some game logic.

Right click the heirarchy and find this text option under UI. 

[IMAGE HERE]

You'll find that doing so actually addds 3 GameObjects to your scene. A **Canvas**, a **Text Object**, and an **EventSystem**.

The **Canvas** is where you are going tpo ut all your UI elements. When you create Text Objects and want them to behave like an overlay, you need to put them on a canvas. Otherwise you will just have free floating text in your game, which may be what you want, but in our case, it is not. 