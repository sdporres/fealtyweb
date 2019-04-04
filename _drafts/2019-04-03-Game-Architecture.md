---
layout: post
title: Game Architecture
---

# Game Architecture

This post is about the technical architecture and design of the Fealty code base. Of the books I have read, Mike Shaffry's Game Coding Complete (https://www.amazon.com/Game-Coding-Complete-Fourth-McShaffry/dp/1133776574) was the msot influential. I read that book many years ago, and today there are many other excellent resources. By "architecture" I mean how the code is organized into components and how the interactions between those components.

Programming games is different from "business" programming in that often you find yourself building something unique that doesn't quite fit existing programming patterns. If things get really gnarly it might mean you made a mistake defining your component interfaces - but nevertheless there are often cases where creativty is needed to come up with a solution. Often our experience with a previous problem will be the key for fixing the current problem. If you are familiar with the MVVC design pattern you will recognize it here, along with the Observer, Repository, Command and few others.

## Considerations

The design of the architecture is informed by the needs of the progrsm of course. In the case of Fealty, there are a few important considerations:

1. I want the client to run on multiple platforms (mobile and PC)

2. Users should be able to play connected to the Fealty server, or not

3. The "game logic" part of the code (e.g. Move this characer, Collect taxes) needs to be run by both the client (what the user interacts with) and the server. Why this is so will become clear soon, but the design implecations are that the game logic needs to be able to run without knowing too much about its context.

4. Users (including the server as a "user") need to be able to fast-forward and rewind the simulation. (Similar to http://subterfuge-game.com/) This is the kind of functionality that is easy to do, if you think about it early enough, or very painful. Planning for it ahead of time, it meant that all the changes in the simulation need to be explicit (so they can be applied and unapplied) and fully deterministic.

## Unity (e.g. IFPGApp)

Unity acts as the interface between the Fealty code and whatever system the code is running on. Things like local file system, networking, and audio/video resources, etc. Unity also offers many features that we cannot use - things like Physics, TileMaps, etc. The reason that the Fealty game code cannot use these Unity features is that then the Fealty code would be dependent on the UnityEngine library. This would mean that the server would also need to reference the Unity library. This is not a technical problem as much as one about being tied to Unity, licensing, etc. Instead, I have either written our own in house systems (like FPGPhysics) that can run anywhere c# code can.

Even though we impose some limitations on Unity, what it does offer is fantastic for a solo dev. First of all, Unity allows us to deploy to most any platform you could want - and I can make iOS builds through the Unity cloud build system. Second is fast iteration times on UI and an easy way to support platform-specific UI. The Unity Scene system enables us to put all the core game stuff in one scene, and build out additiona scenes with all the UI layouts. Each layout scene uses the same MonoBehavior script - the only different is its look and behavior. The WYSIWYG editor is nice as well for lining things up just right.

The FPG (Fifth Power Games) codebase has a MonoBehavior called FPGApp which is fairly boring class that manges the system resources and implements the interface IFPGApp. The app also has a reference to an instance of type IFPGGAmeSDK.(Which is the next major component we are going to talk about) A good example that illustrates how these two layers (FGAPP/Unity and IFPGGameSDK/Fealty) interact is how the game data is made available. After the system level resources are ready, FPGApp loads the game specific resources (art, sound, text) and initializes the IFPGGameSDK object. The Fealty game code expects data, but it itself does not know how to access the local file system. In other words, it doesnt know or care how the data is stored - it just needs it before it can do its thing. This type of clear boundary is possible by using the interfaces (IFPGApp, IFPGGameSDK) instead of conrete class types.

If I ever wanted to ditch Unity, all I would have to rewrite would be FGAPP - all the rest of the code would stay the same.

## FealtyClientSDK (e.g. IFPGGameSDK)

The FealtyClientSDK is the component that defines everything specific to Fealty. It manages all the game data, all the possible player inputs, determining that a sound should be played or what text should be drawn - everything! We have already gone over how the FealtyClientSDK knows about the IFPGApp type, and hwo it can use it to do things with system resources. The other side of the coin is this object also manages the context in which the user is playing. This context determines exactly how all the game stuff is handled. I call this context the PlayerMeta.

Here is an example that illustrates the flow that I have tried to explain so far:

1. Player taps Login button
2. FPGUnityApp processes the input, and translates it into a Command that it passes to the FealtyClientSDK
3. FealtyClientSDK calls Game Logic to Validate the Command, and passes it on to the PlayerMeta
4. PlayerMeta calls Game Logic to Validate the Command, and Execute it to produces Changes
5. PlayerMeta passes the Changes back to the FealtyClientSDK
6. FealtyClientSDK passes changes to FPGUnityApp
7. Unity objects (UI and game enties) are updated

## LocalMeta, RemoteMeta (e.g. IPlayerMeta)

What is important about this flow is that the PlayerMeta could either be a Local (no server connection) or Remote. When the PlayerMeta is Local, the code has to change data and make sure everything is persisted. The Remote meta, on the other hand, sends messages to the server and handles responses - it doesnt know anything about persisting itself.

## KingdomGameDomain, PlayerAccountDomain (e.g. game logic)

The actual game logic, the bits of code that describe the game rules that make Fealty what it is, is broken up into classes along domain lines. Each of these is a static state-less object with static methods that define operations related to concept. The DynastyDomain object defines all the operations for Dynasties. These objects are very simple, and can be called from anywhere. So the Local player meta can use them, as well as the FPGServer code.

## Game Server

[By 'game server' I mean all the different pieces of code and physical hardware that makes the game work]

I won't go into detail about the server, but you can think of it as a hybrid of IGameSDK and IPlayerMeta from an architectural point of view. The game servers need to store and retrieve the game data, spin simulations up and down to validate player actions, coordinate game state changes between all the relevant players, handle social functions like messaging, etc.

---

Now that we have gone over the concept and our design goals, we are turning our full attention to the Kingdom Game. Next time we will talk about the Kingdom Game prototype design, and our roadmap for the near future.

-FealtyDev

![FealtyDevPortrait](/public/images/fealtydevportrait.jpeg){: .portrait }