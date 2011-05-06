Description
-----------

A simple script that manages incremental backups in a local machine. Source
can be remote (via ssh).

Usage
-----

	replica 0.1 by André Restivo (andre.restivo@gmail.com)

	Usage: replica -d <destroot> [-s <sourceroot>] -t <target> [-v] [-b <logfile>] [-r <retries>] [-w <wait]

		-d 	Directory where backups and log files will be created (unless -b is used).
		-s	Directory where source target can be found. Can be a remote location 
			using ssh. If source is a remote location we cannot verify if contents 
			have changed before executing the rsync command and a new directory will 
			always be created. Default: current directory.
		-t	Source target.
		-b 	Alternative log file.
		-r 	How many times to retry a remote rsync.
		-w 	How many seconds to wait between retries.
		-v	Detailed output for testing
		-h	This help message.

	Example: replica -d backups -s /home/johndoe/Documents/ -t work -v

		Creates an incremental backup of /home/johndoe/Documents/work in 
		./backups/work and stores the backup log in ./backups/.replica.log

	Example: replica -d backups -s johndoe@work:~/Documents/ -t stuff -v -b backup.log

		Creates an incremental backup of /home/johndoe/Documents/stuff
		found at server work in ./backups/stuff and stores the backup log 
