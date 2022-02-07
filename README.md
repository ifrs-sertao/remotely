## Remotely - uma alternativa auto-hospedada ao Teamviewer
Este docker-compose sobe o Remotely usando a imagem latest oficial. O Remotely é uma alternativa opensource e auto-hospedada ao Teamviwer ou AnyDesk com recursos bem interessantes como chat integrado, upload de arquivos, execução de scripts e leitura de logs remotos. [Aqui o site oficial do projeto](https://remotely.one/).

## Requisitos
**Este projeto aproveita uma configuração do Traefik já existente**, portanto requer configurações a parte do Traefik configurado com Lets Encrypt. [AQUI uma implementação do Traefik em Docker](https://github.com/ifrs-sertao/traefik-letsencrypt) útil para este projeto.

Uma alternativa é incluir no mesmo docker-compose as configurações do proxu reverso, seguindo a [documentação oficial do Traefik](https://doc.traefik.io/traefik/user-guides/docker-compose/basic-example/).

## Configurações básicas
Ajuste o arquivo docker-compose.yml para refletir as suas configurações, com atenção especial ao domínio no LABEL e a NETWORK (no caso de utilizar o proxy reverso)
```shell
services:
  remotely-prod:
    image: translucency/remotely:latest
    #command: -H unix:///var/run/docker.sock
    restart: always
    ports:
      - 5000:5000
    volumes:
      - ./data/remotely-data:/remotely-data
    # ATENÇÂO - NÂO ESQUEÇA ALTERAR O NOME DO SERVIÇO NAS ROTAS SENÃO QUEBRA AS OUTRAS APLICAÇÕES 
    # (ex: troque traefik.http.routers.PORTAINER..... por um nome representativo e único da sua aplicação  ) 
    labels:
      - "traefik.http.routers.remotely-http.rule=Host(`remoto.<SEU_DOMINIO>`)"
      - "traefik.http.routers.remotely-http.entrypoints=web"
      - "traefik.http.routers.remotely-http.middlewares=redirect"
      - "traefik.http.routers.remotely-https.rule=Host(`remoto.<SEU_DOMINIO>`)"
      - "traefik.http.routers.remotely-https.entrypoints=web-secure"
      - "traefik.http.routers.remotely-https.tls=true"
      - "traefik.http.middlewares.redirect.redirectscheme.scheme=https"
      - "traefik.http.routers.remotely-https.tls.certresolver=letsencrypt"
      - "traefik.http.services.remotely-http.loadbalancer.server.port=5000"
      - "traefik.enable=true"

    networks:
      - proxy

networks:
  proxy:
     external: true

```
## Rodar

```shell
docker-compose up -d
```
