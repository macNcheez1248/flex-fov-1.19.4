# Flex FOV

![flex-full](https://user-images.githubusercontent.com/116838/55492107-4472bb00-55fc-11e9-99d7-22a84666a0e4.jpg)
![flex-menu](https://user-images.githubusercontent.com/116838/55492108-4472bb00-55fc-11e9-893e-3eb59b6588bf.jpg)
![flex-rubix](https://user-images.githubusercontent.com/116838/55492109-4472bb00-55fc-11e9-9085-2eff2873d8b7.jpg)

An experiment to display any FOV (0-360°) in a modern game.

Continuing where [blinky] left off.  Rather than exposing a myriad of options,
the goal is to provide an intelligent default projection based on the
chosen FOV:

[blinky]:https://github.com/shaunlebron/blinky

```
          0             90           180           270           360 degrees
          |-------------|-------------|-------------|-------------|
straight> |     standard      |    panini     |     mercator      |
or        |-------------------|---------------|-------------------|-> equirect when exactly 360
curved>   |     standard      | stereographic |   winkel tripel   |   for panoramic recording
          |-------------------|---------------|-------------------|
```

We are using [this minecraft mod] as the base for this experiment.

[this minecraft mod]:https://github.com/18107/MC-Render360

## Videos

- [🎥 reducing render time](https://youtu.be/ImXwLXYBImA)
- [🎥 proper camera transforms](https://youtu.be/w6lI39ni7QI)
- [🎥 split comparing panini hybrid](https://youtu.be/ILjnDVxhSFg)
- [🎥 panini hybrid](https://youtu.be/OEmSYSDzdnE)
- [🎥 first demo](https://youtu.be/ZNSW6Ga7Wmo)

## Quick Start

__This currently only works for Windows__.  Run the following to start a game with
the mod installed.

```
gradlew.bat runClient
```

> __NOTE__: Prior to running this, I had Minecraft and Minecraft Forge installed (both 1.11.2).
> But I am not actually sure if this is required, since I believe this gradle
> setup is building the entire game itself from decompiled sources?

## IntelliJ Setup

IntelliJ can be setup to allow autocomplete, which is useful for exploring the
Minecraft/Forge APIs in-place.  If you don't wish to use an IDE, you can explore
the APIs the old-fashioned way using this [Forge javadoc][javadoc] (outdated but
probably mostly relevant).

You have to create your own IntelliJ project since it cannot be easily
version-controlled. I loosely followed [these instructions][intellij]:

1. Run `./gradlew setupDecompWorkspace`
1. Open IntelliJ
1. 'Import Project' > choose our `build.gradle` file
1. View > Tool Windows > Project
1. Right click our `*.iml` file > Import Module
1. Run `./gradlew genIntellijRuns`
1. Restart IntelliJ
1. Run > Edit Configurations
1. Put `-Dfml.coreMods.load=mod.render360.coretransform.CoreLoader` in VM options
1. Application > Minecraft Client > Use classpath of module > `*_main`
1. Run > Run 'Minecraft Client'

The game should start with our mod installed.

[intellij]:http://www.minecraftforum.net/forums/mapping-and-modding/mapping-and-modding-tutorials/2714237-forge-1-11-1-10-setting-up-mod-environment-with
[javadoc]:http://takahikokawasaki.github.io/minecraft-resources/javadoc/forge/1.8-11.14.1.1320/

## Deploying

This will build a jar file that users can install.  (Not currently working
when I try to install to a 1.11.2 forge mods folder.)

```sh
gradlew.bat build
# outputs a jar to build/libs
```
