# ShellHacks

### Show all active connections with their port information
```
sudo netstat -tulpn
```
Explanation:
* netstat (**NET**work **STAT**istics)
* -t TCP (Shows TCP connections)
* -u UDP (Shows UDP connections)
* -l listening (State = LISTEN)
* -p program (Shows Program Name/PID)
* -n numeric (Ex: Shows localhost as 127.0.0.x)

### Archive using tar
```
tar -czvf archive-name.tar.gz /path/to/directory-or-file-to-be-archived
```
Explanation:
* tar (**T**ape **AR**chiver)
* -c create (archive)
* -z gzip (use gzip compression format)
* -v verbose (list all files processed)
* -f file archive (use file archive, tar can also write archives to tapes!)

```
tar -czvf archive-name.tar.gz /path/to/input1 /path/to/input2 --exclude=path/to/unnecessary/files-or-dirs --exclude=regex 
```
* regex can be like '*.sh' which will exclude all files ending with .sh
* inputs can be files or directories or both 

### Extract tarballs using tar
```
tar -xzvf archive-name.tar.gz
```
Explanation:
* -x extract (given archive)

```shell
tar -xzvf archive-name.tar.gz -C /path/to/output-directory
``` 
* -C change to directory

### Peek contents of tarballs
```
tar -tvzf archive-name.tar.gz
```
Explanation:
* -t list the contents of an archive

### Split files using split
```
split -b SIZE -d -a NUM input_file output_chunks_prefix
```
* split - split a file into pieces
* -b put SIZE bytes per output file
* -d use numeric suffixes starting at 0, not alphabetic
* -a generate suffixes of length NUM (default 2)
```
split -n N -de -a NUM input_file output_chunks_prefix
```
* -n generate N chunks output files based on input file size
* -e do not generate empty output files with '-n'
```
split -l N -d -a NUM input_file output_chunks_prefix
```
* -l put N lines/records per output file

### Split files using csplit
```
csplit input.txt --suppress-matched -k -z -f output -b '%02d.txt' '%.%' '/-*-/' '{*}'
```
Explanation:

splits 'input.txt' repeatedly at lines matching pattern similar to '---------' represented by the regex '/-*-/' excluding the first line of input.txt and the lines matching pattern, rest are written to files named 'output01.txt', 'output02.txt' etc..

* csplit - split a file into sections determined by context lines
* '-' can be used to read from stdin
* '/regex/[offset]' - outputs the contents to a file till the line matching the pattern 
* '%regex%[offset]' - ignore the line(s) matched by the pattern
* '{repeat-count} - repeat the previous pattern repeat-count additional times
* --suppress-matched do not output lines matching the specified pattern
* -k do not remove already generated output files when errors are occur in the process
* -z suppress zero-length output files
* -f prefix of output
* -b suffix format of output

### Merge files using cat
```
cat f1 f2 > merged_file
```
* cat - concatenate files and print on the standard output
* \> redirect stdout to target_file
```
cat f?? > merged_file
```
* f?? - matches file names having any two characters starting with f like f01,fab,fa1 etc..
```
cat f* > merged_file
```

### Pull data from remote using scp
``` 
scp -i key.pem -P 22 remote-user@remote-address:/full/path/to/remote/file /local/path/to/save/file
```
``` 
scp -i key.pem -P 22 -r remote-user@remote-address:/full/path/to/remote/dir /local/path/to/save/dir
```
* scp - secure copy (remote file copy program)
* -i identity_file (directly passed to ssh)
* -r recursively copy entire directories (follows sym links encountered)
* -P port (specifies the port to connect to on the remote host)

### Push data to remote using scp
```
scp -i key.pem /path/to/local/file remote-user@remote-address:/full/remote/path/to/save/file
```
```
scp -i key.pem -r /path/to/local/dir remote-user@remote-address:/full/remote/path/to/save/dir
```

### One-line info of any bash utility
```
whatis utility_name
```
* whatis - display one-line manual page descriptions

### Create files of specific size
```
truncate -s SIZE target_file
```
* truncate - shrink or extend the size of a file to the specified size
* -s set or adjust the file size by SIZE bytes (K,M,G,T or KB,MB,GB,TB etc.. units can be used to override)
```
head -c SIZE /dev/urandom > target_file
```
* head - output the first part of files
* -c print the first SIZE bytes of each file (K,M,G,T or KB,MB,GB,TB etc.. units can be used to override)
* \> redirect stdout to target_file

### Pull data from remote using rsync
```
rsync -e "ssh -i key.pem" -Pzavh remote-user@remote-address:/full/path/to/remote/file/or/dir /local/path/to/save/file/or/dir
```
* rsync - a fast, versatile, remote (and local) file-copying tool
* -e specify command for remote shell to use
* -P show progress, keep partially transferred files 
* -z compress file data during the transfer
* -a archive mode, equals -rlptgoD
* -v verbose
* -h output numbers in a human-readable format

### Push data to remote using rsync
```
rsync -e "ssh -i key.pem" -Pzavh /local/path/to/save/file/or/dir remote-user@remote-address:/full/remote/path/to/save/file/or/dir
```
### Search for files/directories
```
find -L /path/to/search -maxdepth 5 -type f -iname "*.pdf" -mtime -7 -size +25k -ls
```
* find - search for files in a directory hierarchy
* -L Follow symbolic links
* -maxdepth Descend at most levels (a non-negative integer) levels of directories below the starting-points
* -type **f** for regular file, **d** for directory, **s** for socket
* -iname Base of file name, the match is case insensitive
* -mtime File's data was last modified **n*24** hours ago (+n for greater than n, -n for less than n, n for exactly n)
* -size File uses n units of space, rounding up (k for for kibibytes[KiB], M for mebibytes[MiB], G for gibibytes[GiB])
* -ls if matches, list current file in **ls -dils** format on standard output

### Execute any command with stdin as input
```
ls *.txt | xargs -d "\n" -t tar -cvzf text_files.tar.gz
```
* xargs - build and execute command lines from standard input (default command is  */bin/echo*)
* -d delim Input items are terminated by the specified character
* -t Print the command line on the standard error output before executing it

### View bad login attempts
```
lastb user_name
```
* lastb - shows a log of the /var/log/btmp file, which contains all the bad login attempts

### Show currently logged in users
```
w
```
* w - Show who is logged on and what they are doing
