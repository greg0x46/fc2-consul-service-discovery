#### Perguntas a se fazer (contexto microserviços e autoscaling)

- Qual máquina chamar ?
- Qual porta utilizar ?
- Preciso saber o IP de cada instância ?
- Como ter certeza se aquela instância está saudável ?
- Como saber se tenho permissão para acessar ?


#### Service Discovery

- Descobre máquinas disponíveis para acesso.
- Segmentação de máquinas para garantir segurança.
- Resoluções via DNS.
- Health check.
- Como saber se tenho permissão para acessar.


#### Hashicorp Consul

- Service discovery
- Service segmentation
- Load balancer na borda (layer 7)
- Key/Value configuration
- Opensource / Enterprise
- Mutual tls
- Service regisgry centralizado
- DNS Server


*Agent*: Processo que fica executando em todos nós do cluster. Pode estar sendo executado em Client Mode ou Server Mode.
*Client*: Registra os serviços localmente, Health check, encaminha as informações e configurações dos serviços para o Server.
*Server*: Mantém o estado do cluster, registra os serviços, membership (quem é client e quem é server), retorno de queries (DNS ou API), troca d einformações entre datacenters, etc.
*Dev Mode*: Utilizado para testar features exemplos, roda como servidor, não escala, registra tudo em memória.

#### Comandos

`consul agent -server -bootstrap-expect=<qtd-clusters-esperados> -node=<nome-do-node> -bind=<ip-do-server> -data-dir=/var/lib/consul -config-dir=/etc/consul.d`: Sobe um agent no modo server.
`consul agent -bind=<ip-do-server> -data-dir=/var/lib/consul -config-dir=/etc/consul.d`: Sobe um agent no modo client.
`consul join <ip-remoto>`: Víncula um cluster a um server.
`consul agent -bind=<ip-do-server> -data-dir=/var/lib/consul -config-dir=/etc/consul.d retry-join=<remote-ip>`: Sobe um agent no modo client e entra e se víncula ao cluster, é possível passar vários retry-join.
`consul reload`: Recarrega configurações.
`consul keygen`: Gera uma chave para encriptação.