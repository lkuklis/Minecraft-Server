# Minecraft-Server

Server based on Microsoft Azure Minecraft Server Template.

# Start/Stop Server
```sh
sudo systemctl stop minecraft-server
sudo systemctl start minecraft-server
```

# Get Spigot server
Go to  [Spigot Jenkins](https://hub.spigotmc.org/jenkins/job/BuildTools/) and download latest build. Shortcut: [direct link](https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar)

Or just paste this into console of your server:
```sh
cd /srv/
mkdir spigot
cd spigot
wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
```

