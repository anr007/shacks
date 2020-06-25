### To run
```
sudo docker-compose up -d
```
### To check its running
```
sudo docker-compose logs | grep started
```
### To get password
```
sudo docker exec -it <container-id/name> bash
cat nexus-data/admin.password
```

### Create a docker repo in nexus and configure it using nexus ui

### To allow insecure repos
```
cd /etc/docker
nano daemon.json

{
  "insecure-registries" : ["54.169.135.126:8123"]
}
```

### All running containers will be terminated after the following command run
```
sudo docker service restart 
```
### To allow local auth via cli
- Enable the Docker Bearer Token Realm in Nexus Security->Realms Tab
### To fix error storing credentials problem 
```
sudo apt autoremove  golang-docker-credential-helpers
```
### TAG the local image
```
sudo docker tag tfs_objdetv2:latest localhost:8123/tfs_objdetv2:latest
```
### Then, push the local image to nexus repo
```
sudo docker push localhost:8123/tfs_objdetv2:latest
```
### Pull from nexus repo
```
docker login -u admin -p 123 localhost:8123
docker pull localhost:8123/tfs_objdetv2:latest
```

### Reference
- https://www.ivankrizsan.se/2016/06/09/create-a-private-docker-registry/
- https://docs.docker.com/registry/insecure/
