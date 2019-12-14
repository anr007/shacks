# ShellHacks

### Show all active connections with their port information
```shell
sudo netstat -tulpn
```
Explanation:
* netstat (**NET**work **STAT**istics)
* -t TCP (Shows TCP connections)
* -u UDP (Shows UDP connections)
* -l listening (State = LISTEN)
* -p program (Shows Program Name/PID)
* -n numeric (Ex: Shows localhost as 127.0.0.x)

### Compress using tar
```shell
tar -czvf archive-name.tar.gz /path/to/directory-or-file-to-be-archived
```
Explanation:
* tar (**T**ape **AR**chiver)
* -c create (archive)
* -z gzip (use gzip compression algo.)
* -v verbose (list all files processed)
* -f file archive (use file archive, tar can also write archives to tapes!)

```shell
tar -czvf archive-name.tar.gz /path/to/input1 /path/to/input2 --exclude=path/to/unnecessary/files-or-dirs --exclude=regex 
```
* regex can be like '*.sh' which will exclude all files ending with .sh
* inputs can be files or directories or both 

### Extract using tar
```shell
tar -xzvf archive-name.tar.gz
```
Explanation:
* -x extract (given archive)

```shell
tar -xzvf archive-name.tar.gz -C /path/to/output-directory
``` 
* -C change to directory


