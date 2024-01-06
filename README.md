# Starcraft 2 backwards compatability patch
Modifies map files to replicate behavior of the live version of Starcraft 2 in patch 4.10.0

Intended for use with latest Sc2 linux binary 4.10.0 to speed up AI competition & training

## How the patch data is created

The patch data includes all game data changes between version 4.10.0 and the target version of StarCraft II.
By applying all the changes to a map, a game client at version 4.10.0 running this map will behave as if the game is at the target version.

1. Game data changes are taken from the Casc storage of the game. One way to do it is by comparing the extracted files at https://github.com/Ahli/sc2xml. The history of this github repo - https://github.com/Ahli/sc2xml/commits/master/ - gives the deltas between individual versions.

1. Game data changes for the target version are applied on top of the patch data for the previous version so that the patch data always contains all game changes since version 4.10.0. This is not a trivial task because:
   * Game changes in a later version may affect changes of a previous version. The affected changes of the previous version are removed from the patch data.
   * Game changes may be based on features of version 5.x which are not present in version 4.10.0 of the game. These are manually translated to features available in version 4.10.0, so that the game client can process them.

1. The patch data is tested by applying the patch to maps and testing them in the environments for bot-vs-bot and human-vs-bot.

## How to apply the patch to a map

1. Get a local copy of the map to be patched
   * If the map is already used in AI Arena, download it from from https://aiarena.net/wiki/maps/#wiki-toc-map-downloads

1. Launch StarCraft II Editor either from "Launch Editor" button in Battle.net application, or by running the executable in the installation folder of the game

1. Open the map in the editor like this - https://www.youtube.com/watch?v=lTBFy-R01Wo

1. Make sure the name of the map ends in "AIE" because some bots and bot frameworks will reject maps with names not ending in "AIE"

1. Get the patch data by downloading the corresponding folder from https://github.com/shostyn/sc2patch/tree/master/Patch

1. Launch an MPQ editor (Download from http://www.zezula.net/en/mpq/download.html)

1. Open the map in the MPQ editor and apply the files from the patch data

1. Test the changes by playing the map. Check if the changes from 
