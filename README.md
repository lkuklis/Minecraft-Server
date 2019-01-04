# Minecraft-Server

Server based on Microsoft Azure Minecraft Server Template.

## Start/Stop Server

```sh
sudo systemctl stop minecraft-server
sudo systemctl start minecraft-server
```

## Get Spigot server

Go to  [Spigot Jenkins](https://hub.spigotmc.org/jenkins/job/BuildTools/) and download latest build. Shortcut: [direct link](https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar)

Or just paste this into console of your server:

```sh
cd /srv/
mkdir spigot
cd spigot
wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
```

## Build Spigot server

This build is prepared for version 1.12 (as this is the current version of bedwars plugin which I want to include)

In spigot directory run

```sh
java -jar BuildTools.jar --rev 1.12
```

If there is no Java 8 then you need to install it... :)
As I am on Ubuntu it will looks like...

```sh
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

And now check if Java 8 is set as default version:

```sh
sudo update-alternatives --config java
```

And now set JAVA HOME path

```sh
sudo vim /etc/environment
```

and put here:

```text
JAVA_HOME="/usr/lib/jvm/java-8-oracle"
```

and after all refresh environment

```sh
source /etc/environment
echo $JAVA_HOME
```

Now for a sake of be safe, make a copy of clean normal Minecraft server

```sh
tar -zcvf minecraft-original-server.tar.gz minecraft_server/
```

And now I will switch the original Minecraft server with Spigot server

```sh
cp spigot/spigot-1.12.jar minecraft_server/server.jar
```

And restart server. Viola! Spigot server in run. But it was a simple part. Now I am gonna to extend server with BedWars plugin.

## Map

Download some "lobby" type map. [planetminecraft.com](https://www.planetminecraft.com/resources/projects/tag/lobby/?order=order_popularity)
I selected [this](https://www.planetminecraft.com/project/mini-games-lobby/)

Of coruse you can create you own one.

## Set op

In ops.json

```json
[
  {
    "uuid": "00000000-0000-0000-0000-000000000000",
    "name": "YourNameHere",
    "level": 4
  }
]
```

## Set always day

```sh
/gamerule doDaylightCycle false
```

## Set spawn point

```sh
/mv set spawn
```

## Plugins

I want to include some plugins to make server more fancy :)

- [WorldGuard](https://dev.bukkit.org/projects/worldguard)
- [WorldEdit](https://dev.bukkit.org/projects/worldedit/)
- [PermissionsBukkit](https://bukkit.org/threads/admn-dev-permissionsbukkit-v2-0-official-default-groups-plugin-1-5-2-r1-0.26785/)
- [Multiverse](https://dev.bukkit.org/projects/multiverse-core)
- [Multiverse SignPortals](https://dev.bukkit.org/projects/multiverse-signportals)
- [Multiverse Portals](https://dev.bukkit.org/projects/multiverse-portals)
- [VoidGenerator](https://www.spigotmc.org/resources/voidgenerator.25391/)
- [BedWars](https://dev.bukkit.org/projects/bedwars/)
- [SpawnTP](https://dev.bukkit.org/projects/spawntp)

 [Bungee Tools](https://www.spigotmc.org/resources/bungee-tools-only-hubcommand.84/)

```sh
 wget -O WorldGuard.jar https://dev.bukkit.org/projects/worldguard/files/latest
 wget -O WorldEdit.jar https://dev.bukkit.org/projects/worldedit/files/latest
 wget -O PermissionEx.jar https://dev.bukkit.org/projects/permissionsex/files/latest
 wget -O Multiverse.jar https://dev.bukkit.org/projects/multiverse-core/files/latest
 wget -O MultiversePortals.jar https://dev.bukkit.org/projects/multiverse-portals/files/latest
 wget -O MultiverseSignPortals.jar https://dev.bukkit.org/projects/multiverse-signportals/files/latest
 wget -O Bedwars.jar https://dev.bukkit.org/projects/bedwars/files/2490139/download
 ```

Restart server to get plugins loaded. When login on server type /bukkit:plugins and it will list all loaded plugins.

Note: WorldGuard works only with WorldEdit plugin installed.

### Multiverse

### Multiverse + VoidGenerator - Empty World

```sh
mv create MAP_NAME normal -g VoidGenerator -t FLAT
```

#### Default lobby

- SpawnTP

#### Create Teleport to other world

Create sign and fill with:

```text
Any text
[mv]
world-name
```

The word "[mv]" should turns green. Then click on sign and beign teleported.

### WorldEdit

### Commands

Items ids - https://www.minecraftinfo.com/idnamelist.htm
Multiverse Permissions - https://github.com/Multiverse/Multiverse-Core/wiki/permissions

PermissionsBukkit - https://bukkit.org/threads/admn-dev-permissionsbukkit-v2-0-official-default-groups-plugin-1-5-2-r1-0.26785/
WorldEdit - Selection - http://wiki.sk89q.com/wiki/WorldEdit/Selection
