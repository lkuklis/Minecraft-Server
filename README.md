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

## Bedwars

Go to [BedWars project download page](https://dev.bukkit.org/projects/bedwars/files)
Currently on the day of creating this tutorial current version is Bedwars v2.6.3.

I created directory for plugin in /srv/plugins

```sh
 wget -O Bedwars.jar https://dev.bukkit.org/projects/bedwars/files/2490139/download
 ```




