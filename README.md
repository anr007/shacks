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

### Extract using tar
```
tar -xzvf archive-name.tar.gz
```
Explanation:
* -x extract (given archive)

```shell
tar -xzvf archive-name.tar.gz -C /path/to/output-directory
``` 
* -C change to directory

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

### Pull data from remote using SCP
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

### Push data to remote using SCP
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

