To install the required dependencies:

1. Install the tmux package:

   From ports: `cd /usr/ports/sysutils/tmux && make install clean`

    With pkg: `pkg install tmux`

2. Install a Java version of your choice. Keep in mind that certain versions of Minecraft require Java 17 or higher. I would recommend using OpenJDK 17 JRE:

    from ports: `cd /usr/ports/java/openjdk17-jre && make install clean`

    With pkg: `pkg install openjdk17-jre`

For the Minecraft server:

1. Create a user for the Minecraft server:
 
    `pw user add -n minecraft -c 'Minecraft Server' -d /usr/local/minecraft -m -s /bin/sh`
  
2. Download the `.jar` file for the Minecraft server version of your choice and place it in the Minecraft user's home directory: `/usr/local/minecraft`

3. Create a tmux configuration file in the Minecraft user's home directory:
   
    `echo "set -g default-terminal screen-256color" > /usr/local/minecraft/.tmux.conf`

4. Enable the startup script via `sysrc minecraft_enable=YES`

   If you chose a custom username, home directory or `.jar` file you can set them via, for example:
   
   `sysrc minecraft_user=example`

   `sysrc minecraft_dir=/home/example`

   `sysrc minecraft_jar=exmample.jar`

   Optionally you can pass custom flags to Java, for example:

   `sysrc minecraft_flags=-Xmx4G`
   
Note: If you do not create the tmux configuration file with this line in it, the server will still run, but Java will throw an exception about not knowing the terminal type upon starting the Minecraft server.

Once you have completed these steps: 

- To start the Minecraft server: `service minecraft start`

- To stop the Minecraft server: `service minecraft stop`

- To check if the server is running: `service minecraft status`

- To attach to the Minecraft server console: `service minecraft attach`
  
  You can now use the console to manage your Minecraft server.
