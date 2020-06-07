# linux_cookbook

For those working command-line on linux systems.


Make sure to read "Command Line Kung Fu: Bash Scripting Tricks, Linux Shell Programming Tips, and Bash One-liners"
by Jason Cameron:
https://www.goodreads.com/book/show/21945897-command-line-kung-fu

Know at least basic forms of sed and awk.
Recommendation: O Reilly's  "Sed & awk Pocket Reference, 2nd edition"


## sed command examples

substitute all dots  with nothing, i.e. remove dots. 

sed 's/\.//g' tmp.txt 

substitute beginning of line with two zeroes, i.e. insert two zeroes:

sed 's/^/00/' tmp.txt 

## unique list
get a unique version of a file
sort tmp.txt | uniq


## docker: remove all stopped containers

List them:

docker ps -a -q --filter status=exited

Delete them:

docker rm $(docker ps -a -q --filter status=exited)

## docker: remove dangling docker images

docker rmi $(docker images --filter "dangling=true" -q --no-trunc)

## mssql server container db :: backup db

BACKUP DATABASE mydbname TO DISK = N'/var/opt/mssql/data/mybackup.bak' with noformat, init, skip, norewind, nounload,compression, stats=10

## mssql server container db :: restore db
	
use master;  RESTORE DATABASE mydbname FROM DISK = N'/var/opt/mssql/data/mybackup.bak' WITH REPLACE
GO

## mssql server container db :: restore to a different database

Taken from 
https://stackoverflow.com/questions/6267273/how-to-restore-to-a-different-database-in-sql-server


~~~~
RESTORE FILELISTONLY FROM DISK='e:\mssql\backup\creditline.bak'

>LogicalName
>--------------
>CreditLine
>CreditLine_log

RESTORE DATABASE MyTempCopy FROM DISK='e:\mssql\backup\creditline.bak'
WITH 
   MOVE 'CreditLine' TO 'e:\mssql\MyTempCopy.mdf',
   MOVE 'CreditLine_log' TO 'e:\mssql\MyTempCopy_log.ldf'

>RESTORE DATABASE successfully processed 186 pages in 0.010 seconds (144.970 MB/sec).
~~~~
