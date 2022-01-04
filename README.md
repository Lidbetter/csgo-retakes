csgo-retakes
=============

[![Build status](http://ci.splewis.net/job/csgo-retakes/badge/icon)](http://ci.splewis.net/job/csgo-retakes/)
[![GitHub Downloads](https://img.shields.io/github/downloads/splewis/csgo-retakes/total.svg?style=flat-square&label=Downloads)](https://github.com/splewis/csgo-retakes/releases/latest)
[![Discord Chat](https://img.shields.io/discord/926309849673895966.svg)](https://discord.gg/zmqEa4keCk)

This is a CS:GO [Sourcemod](http://www.sourcemod.net) plugin that creates a competitive-minded gamemode called retakes. The idea is that the T players spawn in a bombsite with the bomb, while the CT spawn on rotation routes and try to retake the site and defuse the bomb.

**Status: Maintained. Not actively developed.**


## For plugin developers

My goal is to keep the base retakes plugin as simple as possible. See [retakes.inc](scripting/include/retakes.inc) for how to extend the plugin.

Here are some examples of what could be done using those natives:
- different weapon allocation policies (by default, everyone gets an AK/M4, armor/helmet, and a kit)
- change how players get put into teams by changing their "round points", the team ratios, or by changing who is in the waiting queue if the game is full
- change how the bombsite is chosen each round (by default one is randomly picked each round)


## Download
Stable releases are in the [GitHub Releases](https://github.com/splewis/csgo-retakes/releases) section.

You may download the [latest development build](http://ci.splewis.net/job/csgo-retakes/lastSuccessfulBuild/) if you wish. If you report any bugs from these, make sure to include the build number (when typing ``sm plugins list`` into the server console, the build number will be displayed with the plugin version).


## Installation

#### Requirements

**Only Sourcemod 1.9 or later is supported.**

#### Instructions
Download the archive and extract the files to the game server. From the download, you should have installed the following (to the ``csgo`` directory):
- ``addons/sourcemod/plugins/retakes.smx``
- ``addons/sourcemod/translations``
- ``cfg/sourcemod/retakes``

#### Configuration
The file ``cfg/sourcemod/retakes/retakes.cfg`` will be autogenerated when the plugin is first run and you can tweak it if you wish.

You may also tweak the values in ``cfg/sourcemod/retakes/retakes_game.cfg``, which is executed by the plugin each map start.

Here are a few important cvars that are in ``cfg/sourcemod/retakes/retakes.cfg``:
- ``sm_retakes_maxplayers``: maximum number of players allowed in the game at once
- ``sm_retakes_ratio_constant``: what percentage of players go on the T team

You can enable optional addon plugins for more features, read the [Addon Plugins](#addon-plugins) section for more information.


## Building
The build process is managed by my [smbuilder](https://github.com/splewis/sm-builder) project. You can still compile retakes.sp without it in the normal fashion, however.

To compile, you will need:
- [SMLib](https://github.com/bcserv/smlib)

You should make sure you have a relatively recent version of smlib - some changes were made to accommodate sourcemod 1.7 changes. The plugin is currently compiled against sourcemod 1.7.1.


## Creating and Editing Spawns

Edit mode can be launched by using the ``sm_edit`` command (!edit in chat), which requires the map-change admin flag. Doing this brings up the edit menu which makes it easy to modify spawns.

Here is how to operate the spawn editor via commands:
- use ``sm_edit`` to launch into edit mode, this makes more spawn-editing commands avaliable (you shouldn't do this on a live, public server). Example: ``!edit`` in chat on a map whose spawns you want to edit
- use ``sm_new`` to create a new spawn. Example: ``!new ct a`` in chat will create a new CT spawn for bombsite A where you are standing.
- use ``sm_show`` to show the spawns for a site. Example: ``!show a`` in chat will show all spawns for bombsite A.
- use ``sm_delete`` to delete the nearest spawn. Example: ``!deletespawn`` in chat.
- use ``sm_goto`` to go to a spawn. Spawns are indexed from 0 upwards. Example: ``!goto 10`` to go to spawn 10.
- use ``sm_iteratespawns`` to fake ``sm_goto`` commands every few seconds to visit every spawn in the map.
- use ``sm_deletemapspawns`` to delete all spawns for the current map

Note: the plugin automatically saves the changed spawns on map ends to a file in addons/sourcemod/configs/retakes.


## Addon plugins

The following plugins are optional and disabled by default. To enable them move them up from the ``addons/sourcemod/plugins/disabled`` directory to ``addons/sourcemod/plugins``.

#### retakes_sitepicker
This plugin adds a simple admin command sm_site to let an admin pick between bombsites being used. For example, then can type: "!site a" or "!site any".

#### retakes_standardallocator
This plugin provides a simple ``sm_guns`` (!guns in chat) command that lets users choose between regular and silenced M4's and whether they want to ever recieve an AWP. It also randomly gives out a small amount of grenades.

#### retakes_pistolallocator
This plugin is an alternative to retakes_standardallocator (meaning: you shouldn't use both of these plugins, just one!) that makes every round a pistol round and lets players choose which pistol they have.

## Contribution and Suggestions
First, check the [issue tracker](https://github.com/splewis/csgo-retakes/issues?state=open) to ask questions or make a suggestion.
If you have a suggestion you can mark it as an enhancement.

**Style/gameplay design choices that don't have to made here, should not be made here**. Spawns can be edited by anyone running a server. How weapons are given can be set by the natives and forwards provided. Please don't submit requests to change these, since everyone will want something different.

Guidelines
- Create a fork on github, clone that, then create a branch to work on ``git checkout -b mybranchname``
- Follow the code-style already used as much as you can
- Submit a pull request when you're happy with the new feature/enhancement/bugfix
- Favor readability and correctness over all else
- For a moderately advanced feature, it may be simpler to write it as a plugin that uses the retakes natives from [retakes.inc](scripting/include/retakes.inc)
- **Keep it simple, stupid**

### Discord Chat

A [Discord](https://discord.gg/zmqEa4keCk) channel is available for general discussion.
