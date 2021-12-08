## Remotely - uma alternativa auto-hospedada ao Teamviewer
Este docker-compose sobe o Remotely usando a imagem latest oficial. O Remotely é uma alternativa opensource e auto-hospedada ao Teamviwer ou AnyDesk com recursos bem interessantes como chat integrado, upload de arquivos, execução de scripts e leitura de logs remotos. [Aqui o site oficial do projeto](https://remotely.one/).

## Requisitos
Requer configurações do Traefik configurado com Lets Encrypt. [AQUI uma implementação do Traefik em Docker](https://github.com/ifrs-sertao/traefik-letsencrypt) útil para este projeto.

## Rodar

```shell
docker-compose up -d
```
