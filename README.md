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

For a sake of be safe, make a copy of clean normal Minecraft server

```sh
tar -zcvf minecraft-original-server minecraft_server/
```
