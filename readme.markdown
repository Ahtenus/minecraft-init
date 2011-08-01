Initscript for minecraft/bukkit servers
=======================================
A good start if you plan to run a minecraft server using Linux.
Moving this scriptfile to /etc/init.d will start the minecraftserver at boot.

The initscript will make the server use a ramdisk to contain the world.
Ramdisk is a part of the ram mounted as a disk and will speed up the
server especially if you've enabled teleportation. It also has the
ability to backup and clean the server.log. A big logfile slows down the
server alot.


Requirements
------------
screen,rsync

Access server console
=====================

	screen -r minecraft

Exit the console
	
	Ctrl+A D

Setup
=====

1. Move or symlink the script to `/etc/init.d/minecraft`, set the required premissions and update rc.d.

		chmod 755 /etc/init.d/minecraft
		update-rc.d minecraft defaults

2. Mount a ramdisk or use the one already mounted at `/dev/shm/`

3. Move your worlds to the folder specified by `WORLDSTORAGE`

4. Edit crontab

		sudo crontab -e

	and add these lines

		#m 	h 	dom	mon	dow	command
		02 	05 	*	*	*	/etc/init.d/minecraft backup
		55 	04 	*	*	*	/etc/init.d/minecraft log-roll
		*/30 	* 	*	*	*	/etc/init.d/minecraft to-disk

5. Edit the variables in the scriptfile to your needs

Good stuff
==========
[Backup rotation script](https://github.com/adamfeuer/rotate-backups)
