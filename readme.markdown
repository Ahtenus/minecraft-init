Initscript for minecraft/bukkit servers
=======================================
A good start if you plan to run a minecraft server using Linux.
Moving this scriptfile to /etc/init.d will start the minecraftserver at boot.

The initscript will make the server use a ramdisk to contain the world. Ramdisk is a part of the ram mounted as a disk and will speed up the server especially if you've enabled teleportation. It also has the ability to backup and clean the server.log, a big logfile slows down the minecraft server alot, so a regular log rolling is recomended.


Requirements
------------
screen,rsync

Access server console
---------------------

	screen -r minecraft

Exit the console
	
	Ctrl+A D

Setup
=====
There is a couple of things that need to be setup before using the
script, I'm using Ubuntu server 10.10 so if are too just follow along,
else you might need to mount your own ramdisk.

1. Move or symlink the script to /etc/init.d/minecraft

2. Rename your world dir to diskworld and symlink the ramdisk in instead.

		cd ~/minecraft
		mv world diskworld
		ln -s /dev/shm/world world

3. Create the log directory

		mkdir logs

4. Edit crontab

		sudo crontab -e

	and add these lines

		#m 	h 	dom	mon	dow	command
		02 	05 	*	*	*	/etc/init.d/minecraft backup
		55 	04 	*	*	*	/etc/init.d/minecraft log-roll
		*/30 	* 	*	*	*	/etc/init.d/minecraft to-disk

5. Edit the variables in the scriptfile to your needs
