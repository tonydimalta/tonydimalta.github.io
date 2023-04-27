---
title: "How To Learn UE4 & GAS In Two Weeks"
description: "In this guide, I'll explain how I learned Unreal Engine 4 and the Gameplay Ability System in two weeks."
excerpt: "It can feel daunting to learn a new engine/system, especially when joining a new company/project or..."
categories:
  - Unreal
tags:
  - Unreal Engine
  - Gameplay Ability System
slug: learn-UE4-GAS
---

It can feel daunting to learn a new engine/system, especially when joining a new company/project or even when getting started in the video game industry. I'm going to explain how I learned **Unreal Engine 4** and the **Gameplay Ability System** in basically two weeks (at least enough to start working on a complex project), and hopefully it'll prove useful if (or when) you're faced with a similar challenge (i.e. not necessarily on the same engine or system).

# Table of contents
1. [Unreal Engine](#unreal-engine)
  - [Requirements](#requirements)
  - [Recommended](#recommended)
  - [Getting Started](#getting-started)
2. [Gameplay Ability System](#gameplay-ability-system)
3. [Useful Resources](#useful-resources)

## Unreal Engine <a name="unreal-engine"></a>

### Requirements <a name="requirements"></a>
- [Unreal Engine 4 installed](https://docs.unrealengine.com/4.27/en-US/Basics/InstallingUnrealEngine/)

  NB: Installing this way (stock) has one significant drawback, it doesn't allow you to modify the source code or recompile the engine; for learning purposes the stock engine should be fine, but for other purposes (especially if you aim to release on console) then it is recommended to install via the [source code on GitHub](https://github.com/EpicGames/UnrealEngine).

  NB2: If you're installing a stock engine, I would recommend ticking the option to install the *Editor symbols for debugging*, otherwise you won't be able to debug (e.g. put breakpoints) in engine or plugin code; feel free to untick any target platform you're not interested in to save some space.

  [![EditorSymbols]({{ site.url }}{{ site.baseurl }}/assets/images/unreal-install-options-editor-symbols.png)]({{ site.url }}{{ site.baseurl }}/assets/images/unreal-install-options-editor-symbols.png)

### Recommended <a name="recommended"></a>
- IDE of your choice, [Visual Studio](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/) is the one being referenced in most online resources and even the official documentation, but if you're already familiar with another like [Rider](https://www.jetbrains.com/help/rider/Unreal_Engine__Before_You_Start.html) it's perfectly fine.  
- C++ or C/C# knowledge.

  Note that you can still follow this guide while ignoring the code side.

  Also note that **GAS must be set up in C++**, but `GameplayAbilities` and `GameplayEffects` can be created in Blueprint by designers.

There is no way around it, the first step is to get to know the engine. If you have prior knowledge of another engine, it can help smooth up the process, but you can do without it.

NB: If you come from **Unity**, [Unreal Engine For Unity Devs](https://docs.unrealengine.com/4.27/en-US/Basics/UnrealEngineForUnityDevs/) can be a good starting point and/or a reference to keep for later, and Alex Forsythe has a good video on [Unreal vs. Unity](https://youtu.be/iQ3c-lrHO7o).

You'll also need to know how to work with **Unreal C++**, you can reference to [CPP Programming Quick Start](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/CPPProgrammingQuickStart/) to get started (we'll go in more depth later).

⚠️Windows command line has a 1024 character limit and Windows path cannot exceed 256 characters until Windows starts complaining when you try to build/compile a project. To prevent that, you can either create your project in a very short location (e.g. “C:\MyProj”) or to get creative, you can put the files anywhere you want, then symlink to that location (e.g. open the Command Prompt, then type without quotes “mklink /J C:\MyProj C:\Fancy\Custom\Path\MyProject”, but make sure the short folder does not exist yet since the junction will create it).

For your first little project(s), I'd recommend the *Getting Started Series by Tommy Tran*. This is a 10-part tutorial series that contain detailed guides covering the core topics you need to know.

### Getting Started Series by Tommy Tran <a name="getting-started"></a>
1. [Getting Started](https://www.raywenderlich.com/151018/unreal-engine-4-tutorial-beginners)  
2. [Blueprints](https://www.raywenderlich.com/156038/unreal-engine-4-blueprints-tutorial)  
3. [Materials](https://www.raywenderlich.com/165504/unreal-engine-4-materials-tutorial)  
4. [User Interface](https://www.raywenderlich.com/167227/unreal-engine-4-ui-tutorial)  
5. [How to Create a Simple Game](https://www.raywenderlich.com/168091/create-simple-game-unreal-engine-4)  
6. [Animation](https://www.raywenderlich.com/171595/unreal-engine-4-animation-tutorial)  
7. [Audio](https://www.raywenderlich.com/173813/unreal-engine-4-audio-tutorial)  
8. [Particle Systems](https://www.raywenderlich.com/178015/unreal-engine-4-particle-systems-tutorial)  
9. [Artifical Intelligence](https://www.raywenderlich.com/181206/unreal-engine-4-tutorial-getting-started-ai)  
10. [How to Create a Simple FPS](https://www.raywenderlich.com/182606/create-simple-fps-unreal-engine-4)

Tip: Follow them step by step, and if you're really struggling with something, download the completed project and compare with yours to see what you did wrong.

For programmers, you'll also need some **Unreal C++** fundamentals, so you can follow this other guide by Tommy Tran:
- [Unreal Engine 4 C++ Tutorial](https://www.kodeco.com/185-unreal-engine-4-c-tutorial)

Once that's done, you should be familiar with the engine and you can go to the next step. But if you want to potentially explore more tutorials, feel free to browse [Udemy Free Beginner Tutorials](https://www.udemy.com/topic/unreal-engine/?instructional_level=beginner&instructional_level=all&price=price-free&sort=popularity) or [Epic Games Beginner Courses & Tutorials](https://dev.epicgames.com/community/unreal-engine/learning?is_beginner=true&industries=games&types=course,tutorial).

## Gameplay Ability System <a name="gameplay-ability-system"></a>

The next step will depend if you want/need to learn the **Gameplay Ability System** or if you just want to keep building on your early engine knowledge. But before making a decision, let's quickly go over **GAS**.

From the [Official Documentation](https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/GameplayAbilitySystem/):  
> The **Gameplay Ability System** is a highly-flexible framework for building abilities and attributes of the type you might find in an RPG or MOBA title. You can build actions or passive abilities for the characters in your games to use, status effects that can build up or wear down various attributes as a result of these actions, implement "cooldown" timers or resource costs to regulate the usage of these actions, change the level of the ability and its effects at each level, activate particle or sound effects, and more. Put simply, this system can help you to design, implement, and efficiently network in-game abilities as simple as jumping or as complex as your favorite character's ability set in any modern RPG or MOBA title.

***Why should I use it instead of rolling my own system?***  
This system is easy to extend, really efficient in a multiplayer environment, and it makes creating abilities quite easy and intuitive. It has been battle tested in AAA commercial games such as Paragon and Fortnite among others. Epic Games even released some sample projects using it (e.g. [Action RPG](https://docs.unrealengine.com/4.27/en-US/Resources/SampleGames/ARPG/) on UE4, [Lyra](https://docs.unrealengine.com/5.0/en-US/lyra-sample-game-in-unreal-engine/) and [Valley of the Ancient](https://docs.unrealengine.com/5.0/en-US/valley-of-the-ancient-sample-game-for-unreal-engine/) on UE5).

***What's the catch?***  
The system is not really plug-and-play, the initial setup involves writing a lot of initialisation code. Currently, we're missing a standardized way of adding and initializing abilities and attributes, which can be subject to data races in multiplayer games.

If you decided to focus on **Unreal** for the time being and put **GAS** aside, you can still follow the next section but pick a different sample project (e.g. [Survival Game by Tom Looman](https://www.tomlooman.com/unreal-engine-cpp-survival-sample-game/)).

***How do I get started?***  
You could go through the trouble of setting the system up, but what I recommend here (unless you really need/want to set it up yourself, in which case you can use this unofficial [GAS Documentation](https://github.com/tranek/GASDocumentation) as a reference) is to download a sample project. You can pick one from **Unreal** official documentation that I mentioned above (e.g. [Action RPG](https://docs.unrealengine.com/4.27/en-US/Resources/SampleGames/ARPG/)), but I do recommend [GAS Shooter](https://github.com/tranek/GASShooter) as it's the one I personally used.

From there, play around with the game, look at the blueprints and the code, try to understand how it works.

Once you're a bit more familiar with the project, try to follow and repeat the following steps:
1. What can I tweak to make it better?  
2. What can I rework to make a good improvement?  
3. What can I add that seem fun?

***Why am I breaking it down like that?***  
Because personally, I found that starting small and going bigger over time helped with the learning curve, and going back to smaller tasks helped learning more bits and pieces than only focusing on one big task.

***What does it look like?***  
To go back on my own experience, it might look something like that:
1. The lock on the chest takes forever to unlock, and it's frustrating to wait while watching the slow progress bar. Let's try to make it faster.
2. No matter how fast it is, I still don't find it enjoyable. Lets make the lock damageable, so that it will open the chest after being shot with a weapon.
3. If I shoot on the ground below my feet with the rocket launcher nothing happens, I want to add a rocket jump ability!  

For each of these points, you might want to break down what you need to do to achieve the desired result, and take some notes on how you actually did it. That way, you'll make assumptions on the system and see if you were right while keeping track of what you learned along the way.

Repeat the process as much as you want, but keep in mind it's okay if there's something you actually didn't manage to do or figure out, ask for help if you can and switch to something else before it becomes frustrating, you can always go back to it later.

I hope that was useful to you, and good luck on your journey to learn a new engine/system!

### Useful Resources <a name="useful-resources"></a>
- [Epic Coding Standard](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/)  
  *Standards and conventions used by Epic Games in the Unreal Engine 4 codebase*
- [UE Tips & Best Practices](https://flassari.notion.site/UE-Tips-Best-Practices-3ff4c3297b414a66886c969ff741c5ba)  
  *Collection of Tips & Tricks from an AAA Unreal Dev*
- [Unreal Engine C++ Guide](https://www.tomlooman.com/unreal-engine-cpp-guide/)  
  *Comprehensive reference guide for Unreal Engine C++ by Tom Looman*
- [Unreal Engine Gameplay Framework](https://www.tomlooman.com/unreal-engine-gameplay-framework/)  
  *Primer to understanding Unreal’s gameplay classes such as Pawn, Components, GameMode, etc. by Tom Looman*
- [Multiplayer Network Compendium](https://cedric-neukirchen.net/docs/category/multiplayer-network-compendium/)  
  *This compendium is meant to give you a good start into multiplayer programming for Unreal Engine*
- [GAS Documentation](https://github.com/tranek/GASDocumentation)  
  *Unofficial documentation for the GameplayAbilitySystem plugin with a simple multiplayer sample project*
