// using host port 9444 because 9443 was already in use  
// create the network called `prod` first

```
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9444:9443 --name portainer --network prod --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```
