# Docker-Swarm-Lari-Ribeiro
Material de apoio: https://20231-ifba-saj-ads-tawii.github.io/blog-material-aula/posts/10_Orquestracao.html#pod

## Etapas seguidas
### Passo 1

Faça login em https://labs.play-with-docker.com/ para acessar seu terminal PWD

Digite o seguinte comando em seu terminal PWD: 
```
docker run -dp 80:80 docker/getting-started:pwd
```
### Passo 2
```
docker swarm init --advertise-addr 192.168.0.13
```
Mensagem: "Swarm initialized: current node (seu nó) is now a manager", "To add a worker to this swarm, run the following command".
```
docker swarm join --token SWMTKN SEU_TOKEN SEU_IP_DO_NODO_PRINCIPAL:2377
```
Agora seu nó principal pode adicionar cluters.

