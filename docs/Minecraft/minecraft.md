# Minecraft

First we need to create a directory
```bash
mkdir minecraft
```

Next we need to go into this directory we just created to do that we use this command
```bash
cd minecraft
```

Run this command to download the Minecraft Bedrock Server package
```bash
wget https://minecraft.azureedge.net/bin-linux/bedrock-server-1.21.23.01.zip
```

Then we need to install the software to unzip the files
```bash
sudo apt install unzip
```

Then we have to unzip the zip file
```bash
unzip bedrock-server-1.21.23.01.zip
```

After that we can the edit our settings using the nano command
```bash
nano server.properties
```

Once you are do in there you can do Ctrl-X Then Y then enter to save changes

Next we need to start out server. To do that we run this command
```bash
./bedrock_server
```