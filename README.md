# Andrey874_microservices
В процессе выаролнения ДЗ, сделано следующее:  
- Установлен Docker:  
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -  
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io  
```
- Запущен первый контейнер:  
`docker run hello-world`  
- Создан image из контейнера:  
`docker commit <u_container_id> yourname/ubuntu-tmp-file`  
- Создана ВМ на базе yandex cloud, для удаленного разворачивания docker:
``` yc compute instance create \
  --name docker-host \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --ssh-key ~/.ssh/id_rsa.pub
  ```
  - Создан docker-machine на удаленном хосте yandex cloud:
  ```docker-machine create \
  --driver generic \
  --generic-ip-address=130.193.39.51 \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/id_rsa \
  docker-host
  ```
- Написан Dockerfile для создания образа с работающим приложением
- Созданный image загружен в docker hub https://hub.docker.com/repository/docker/andrey874/otus-reddit  

