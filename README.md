## Boirlerplate implantação de aplicações por trás do Treafik 2.4 com ICP Edu Ativo
Este projeto pode servir de base para implantações de aplicações em que se deseje expor usando o proxy reverso Traefik com as configurações 
do ICP Edu  do campus.


A implementação é bem simples, basta incluir alguns campos nos LABELS, vincular a rede traefik-net e o Traefik faz o resto. Não precisa reinciar o Traefik!

### Pontos de Atenção 

- [ ] Ajustar as regras de Host para o domínio correto da tua aplicação ```traefik.http.routers.portainer.rule=Host(`remotely.yourdomain.com```
- [ ] O domínio precisa ser resolvido por um servidor DNS válido
- [ ] Caso o serviço exponha mais de uma porta, é obrigatório setar a porta padrão nos Labels ```traefik.http.services.remotely.loadbalancer.server.port=9000"```
- [ ] Em nosso cenário, configurações de websecure e tls são obrigatórios
- [ ] Mapeie a rede traefik-net (obrigatório) e seus volumes 
