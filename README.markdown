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

Log Files
---------

The log file can have lines in the following formats:

	[<target>] <date>.<time> (<size>): Full backup complete (<duration>)
	[<target>] <date>.<time> (<size>): Incremental backup from <previous> complete (<duration>)
	[<target>] <date>.<time> (<size>): Failed backup (<duration>) Giving up
	[<target>] <date>.<time> (<size>): Failed backup (<duration>) Retrying in <wait>

target - the target being backed up
date - the execution date in the format yyyymmdd
time - the execution time in the format HHMMss
size - The size of the backup
duration - How much time did the operation take
previous - The directory that served as a base for the incremental backup
wait - How much time until we retry
