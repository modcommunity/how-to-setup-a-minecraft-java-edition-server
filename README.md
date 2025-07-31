A full guide on how to set up a **Minecraft Java Edition server** on both **Windows** and **Linux (Debian 12)**! This includes installing Java, basic server configuration, and launching the server via startup scripts or using tools like `screen` on Linux.

[**View Guide On TMC (Recommended Due To Better Formatting)**](https://blog.moddingcommunity.com/how-set-up-a-minecraft-java-edition-server/)

Whether you're looking to host a small survival server for your friends or create a public modded world, this guide will walk you through what you need to start out!

## Table Of Contents
* [Requirements](#requirements)
* [Download Minecraft Server JAR](#download-minecraft-server-jar)
* [Setting Up On Windows](#setting-up-on-windows)
    * [Install Java](#install-java-on-windows)
    * [Create A Startup Script](#create-a-startup-script-windows)
* [Setting Up On Debian Linux (Debian 12)](#setting-up-on-linux-debian-12)
    * [Install Java](#install-java-on-linux)
    * [Create A Startup Script](#create-a-startup-script-linux)
    * [Using `screen`](#using-screen-on-linux)
* [Basic Configuration](#basic-configuration)
* [Conclusion](#conclusion)
* [See Also](#see-also)

## Requirements
Before setting up your server, here's what you'll need:

* A PC with **4GB or more RAM**
* A [Minecraft Java Edition](https://www.minecraft.net/en-us/store/minecraft-java-edition) account
* [Java 17](https://adoptium.net/) or newer (depending on Minecraft version)
* If you want other players to be able to join the server, you will need to ensure you have a stable Internet connection and TCP port `25565` port forwarded on your network. [Here's](https://portforward.com/minecraft/) a guide on how to port forward!

Additionally here's a list of nice haves.

* A basic understanding of how to run scripts and commands (Batch for Windows, Bash/Shell for Linux).
* Familiarity with your terminal or command prompt.

## Download Minecraft Server JAR
You'll need the official Minecraft Server `.jar` file:

* Go to: [https://minecraft.net/en-us/download/server](https://minecraft.net/en-us/download/server)
* Download the latest `.jar` file and place it in a new folder. We recommend something like:

```
C:\MinecraftServer
```
or on Linux:
```
~/minecraft/server
```

## Setting Up On Windows

### Install Java On Windows
1. Download Java 17+ from [Adoptium](https://adoptium.net/temurin/releases/)
2. Run the installer
3. (Optional) Add Java to your system `PATH`:
    ```bat
    setx PATH "%PATH%;C:\Program Files\Eclipse Adoptium\jdk-17\bin"
    ```

### Create A Startup Script (Windows)

Inside the folder where your `server.jar` is located:

1. Right-click → New → Text Document  
2. Rename it to `start.bat`  
3. Edit it and paste the following:

    ```bat
    @echo off
    java -Xmx4G -Xms2G -jar server.jar nogui
    pause
    ```

4. Save the file and double-click `start.bat` to launch your server.

If it's your first run, a `eula.txt` file will appear. Open it and change:
```text
eula=false
```
to:
```text
eula=true
```

Then re-run `start.bat`.

## Setting Up On Linux (Debian 12)

### Install Java On Linux
Open a terminal and type:

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk
```

Verify it installed:

```bash
java -version
```

### Create A Startup Script (Linux)

Create a new folder and move into it:

```bash
mkdir -p ~/minecraft/server
cd ~/minecraft/server
```

Move your `server.jar` here, then create `start.sh`:

```bash
nano start.sh
```

Paste this:

```bash
#!/bin/bash
cd "$(dirname "$0")"
java -Xmx4G -Xms2G -jar server.jar nogui
```

Save and make it executable:

```bash
chmod +x start.sh
```

Run it with:

```bash
./start.sh
```

Just like Windows, the first time you run it you'll need to accept the EULA:

```bash
nano eula.txt
```
Change `eula=false` to `eula=true`, then save and re-run.

### Using `screen` On Linux

If you want your server to keep running after you close the terminal:

1. Install screen:
```bash
sudo apt install screen
```

2. Start a new session:
```bash
screen -S minecraft
```

3. Run your server:
```bash
./start.sh
```

4. Detach from screen:  
Press `CTRL + A`, then `D`

5. Reattach later:
```bash
screen -r minecraft
```

This is a great way to keep your server online 24/7 even when you're not SSH'd in.

## Basic Configuration

After running your server once, it will generate a `server.properties` file.

To edit the configuration:
```bash
nano server.properties  # Linux
notepad server.properties  # Windows
```

Some options you may want to change:

```properties
motd=Welcome to My Server!
max-players=10
difficulty=normal
pvp=true
enable-command-block=false
allow-nether=true
online-mode=true
```

You can whitelist users by adding them via the server console or editing `whitelist.json`:

```bash
whitelist on
whitelist add <username>
```

## Conclusion
You now have a basic, but functioning **Minecraft Java Edition server** running on either Windows or Linux! Whether you're hosting a private world for friends or planning to go public, you should be off to a great start.

## See Also
* [Minecraft Java Server Download](https://www.minecraft.net/en-us/download/server)
* [OpenJDK Downloads (Linux)](https://openjdk.org/)
* [Adoptium Java Downloads (Windows)](https://adoptium.net/)
* [How To Port Forward Minecraft](https://portforward.com/minecraft/)
* [Screen Manual](https://linux.die.net/man/1/screen)

This guide is a *work-in-progress* and may be updated over time. If you have suggestions or improvements, we'd love your feedback!