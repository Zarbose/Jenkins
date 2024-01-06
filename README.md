# Jenkins

### Build de l'image
```bash
docker build -t myjenkins -f jenkins.Dockerfile .
```

### Création du network
```bash
docker network create jenkins
```

### Lanement du container
```bash
docker run \
  --name myjenkins \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins
```

### Obtenir le premier mot de passe
```bash
docker exec myjenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### Stop et start du container
```bash
docker stop myjenkins
docker start myjenkins
```
