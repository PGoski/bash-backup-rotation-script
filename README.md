##[Tonjoo](http://tonjoo.com/backup-rotation-script/ "Tonjoo") - Bash Backup Rotation Script

###Description
This script allow you to create a rotation backup for your files and mysql database. The backup target can be local or remote (FTP). 

The script have 3 `backup type`

- Daily backup
- Weekly backup (default : perform every sixth day of the week)
- Monthly backup (default : perform every first day of the month)

This script provide you customize the where to backup of each `backup type`. For example you can choose to do daily and weekly backup on local machine and monthly backup on FTP server.

Each type of backup will have a backup retention(copy). The default retention for every type of backup can be configured. 

The backup retention default day is :

*   Daily backup : 3 Day ( 3 daily backup )
*   Weekly backup : 14 Day ( ~2 weekly backup )
*   Monthly backup : 30 Day ( ~1 Monthly backup )

Please consider your space when creating many retention.

###Table of Content
1. [Usage Instruction](#usage_instruction)
2. [Backup Type Configuration](#backup_type_configuration)
3. [FTP Backup Configuration](#ftp_backup_configuration)
4. [Contribute and Contact](#contribute_and_contact)

<div id='usage_instruction'>
##1. Usage Instruction

1. Download the `backup_rotation.sh` script into your NIX server.

		wget https://raw.github.com/todiadiyatmo/bash-backup-rotation-script/master/backup_rotation.sh

2. Open the file using your favourite editor (ex :`nano` or `vi`)

		nano backup_rotation.sh

	or
	
		vi backup_rotation.sh	 

3. Edit the configuration file. MYSQL configuration, for minimal `BACKUP_DIR`, `TARGET_DIR` must be filled. 

		# The directory to be backup , DO NOT END THE DIRECTORY WITH BACKSLASH ! 
		TARGET_DIR=/target_directory
		
		# The backup directory , DO NOT END THE DIRECTORY WITH BACKSLASH ! 
		BACKUP_DIR=/your_backup_direcory
		
		# Admin email
		MAIL="your_email@email.com"
		
		# Number of day the daily backup keep
		RETENTION_DAY=3
		
		# Number of day the weekly backup keep
		RETENTION_WEEK=14
		
		# Number of day the monthly backup keep
		RETENTION_MONTH=30
		
		#Monthly date backup option (day of month)
		MONTHLY_BACKUP_DATE=1
		
		#Weekly day to backup option (day of week - 1 is monday )
		WEEKLY_BACKUP_DAY=6

4. Make the script executable

		chmod +x backup_rotation.sh

5. Test the script 

		sh backup_rotation.sh

6. If the script running correctly the file will be available on `TARGET\_DIR`. Try to extract the file and check the content

		tar -xzfv [filename].tgz

7. To make the backup running daily, put it on the crontab
	
		#run crontab
		crontab -e

		#put this line on crontab 
		0 0 * * * sh [path to your backup_rotation.sh ]

8. If crontab not available, install `cronie` package first (CentOS)

		yum install cronie

<div id='backup_type_configuration'>
##2. Backup Type Configuration

To customize the `backup type` you must alter the `LOCAL_BACKUP_OPTION` and `FTP_BACKUP_OPTION` in the configuration script.

The configuration value of `LOCAL_BACKUP_OPTION` and `FTP_BACKUP_OPTION` can be view on the table below

![Backup type configuration](http://tonjoo.com/wp-content/uploads/2013/09/tuts.png)

For example, if you want to do daily on local and week on FTP you must fill both options with this value

	LOCAL_BACKUP_OPTION=1
		
	FTP_BACKUP_OPTION=2

<div id='ftp_backup_configuration'>
##3. FTP Backup Configuration

1. Make sure that you fill the `FTP_BACKUP_OPTION` with correct value
2. Fill the FTP configuration on the script 

		# -----------------
		# FTP Configuration
		# Enter all data within the ' ' single quote !
		# -----------------
		
		#This is the FTP servers host or IP address. 
		FTP_HOST='FTP HOST' 
		
		#FTP PORT
		FTP_PORT=21
		
		#This is the FTP user that has access to the server. 
		FTP_USER='FTP USER'           
		
		#This is the password for the FTP user. 
		FTP_PASSWORD='FTP_PASSWORD'          
		
		#The backup directory on remote machine, DO NOT END THE DIRECTORY WITH BACKSLASH ! 
		FTP_TARGET_DIR='/remote_path'

<div id='contribute_and_contact'>
##4. Contribute and Contact

Everybody is welcome to fork and contribute. If you need to pull something just post it on the message board. 