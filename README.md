# ShellHacks

### Show all active connections with their port information
```shell
sudo netstat -tulpn
```
Explanation:
* netstat (**Net**work **Stat**istics)
* -t TCP (Shows TCP connections)
* -u UDP (Shows UDP connections)
* -l listening (State = LISTEN)
* -p program (Shows Program Name/PID)
* -n numeric (Ex: Shows localhost as 127.0.0.x)
