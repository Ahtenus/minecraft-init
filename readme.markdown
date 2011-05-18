Initscript for minecraft/bukkit servers
=======================================
A good start if you plan to run a minecraft server on linux.
Moving this scriptfile to your /etc/init.d starts the minecraft server at boot.

Requierments
------------
screen,rsync

Get to the server console
-------------------------

	screen -r minecraft

Setup
=====
There is a couple of things that need to be setup before using this
initscript, I'm using Ubuntu server 10.10 so if are too just follow along.

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

		m 	h 	dom	mon	dow	command
		02 	05 	*	*	*	/etc/init.d/minecraft backup
		55 	04 	*	*	*	/etc/init.d/minecraft log-roll
		*/10 	* 	*	*	*	/etc/init.d/minecraft to-disk

5. Edit the variables in the scriptfile to your needs
