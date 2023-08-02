# Docker-Swarm-Lari-Ribeiro

Material de apoio: https://20231-ifba-saj-ads-tawii.github.io/blog-material-aula/posts/10_Orquestracao.html#pod

## Etapas seguidas

### Passo 1

Faça login em: https://labs.play-with-docker.com/ 
Para acessar seu terminal PWD

Digite o seguinte comando em seu terminal PWD: 
```
docker run -dp 80:80 docker/getting-started:pwd
```
### Passo 2

Crie 2 instâncias,uma para iniciar o docker swarm e outra para ser adicionada a ele, posteriormente.

Inicialize o docker swarm com o IP recebido
```
docker swarm init --advertise-addr 192.168.0.13
```
Mensagem: "Swarm initialized: current node (seu nó) is now a manager", "To add a worker to this swarm, run the following command".

Após Inicializar, foi informado 2 comandos
(os tokens informados abaixo são exclusivos do meu container).

Para adicionar um worker
```
docker swarm --token SWMTKN-1-5g8qn5qxgz2mpqxt5v85zmgoyxuo47pq48achrolfv4o95z1k6-9oktmygvtcnfryt6ctpsogmazz 192.168.0.13:2377
```

Para adicionar um manager
```
docker swarm join --token manager 
```
```
docker swarm join --token SWMTKN-1-5g8qn5qxgz2mpqxt5v85zmgoyxuo47pq48achrolfv4o95z1k6-otu4knurninp3mt4zu9vxfsi3 192.168.0.13:2377
```
Verifique o número de nós e suas informações com o comando
```
docker node ls
```

### Passo 3

Criar e colocar uma pilha de serviços no docker swarm

Crie um arquivo chamado docker-compose.yml com o seguinte conteúdo fornecido no blog de aulas:

```
version: '3.8'
services:
  web:
    image: sua_imagem_web:latest
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
    ports:
      - "80:80"
    networks:
      - webnet

  db:
    image: sua_imagem_db:latest
    deploy:
      replicas: 1
      restart_policy:
        condition: on-failure
    environment:
      MYSQL_ROOT_PASSWORD: senha_root
      MYSQL_DATABASE: nome_do_banco
    networks:
      - webnet

networks:
  webnet:
```

Modifique as imagens "sua_imagem_web:latest" e "sua_imagem_db:latest", colocando uma de sua escolha.

Eu substitui pelas imagens oficiais disponíveis no docker do solr e o mysql

Por fim, implante o arquivo criado com o seguinte comando.
```
docker stack deploy -c docker-compose.yml minha_pilha
```


