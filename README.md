# Deploy Wazuh Docker in single node configuration

This deployment is defined in the `docker-compose.yml` file with one Wazuh manager containers, one Wazuh indexer containers, and one Wazuh dashboard container. It can be deployed by following these steps: 

1) Increase max_map_count on your host (Linux). This command must be run with root permissions:
```
$ sysctl -w vm.max_map_count=262144
```
2) Run the certificate creation script:
```
$ docker-compose -f generate-indexer-certs.yml run --rm generator
```
3) Start the environment with docker-compose:

- In the foregroud:
```
$ docker-compose up
```
- In the background:
```
$ docker-compose up -d
```

The environment takes about 1 minute to get up (depending on your Docker host) for the first time since Wazuh Indexer must be started for the first time and the indexes and index patterns must be generated.
# Wazuh SIEM Deployment & Log Ingestion 🛡️ 

Este projeto documenta a implementação de uma solução de monitoramento de segurança centralizada (SIEM) utilizando **Wazuh 4.10.0** e **Docker** em ambiente **Arch Linux**. O laboratório faz parte da formação em CyberSecurity (Google/Coursera).

## 🚀 Objetivo
Configurar um pipeline de ingestão de logs históricos para análise de eventos de segurança, simulando o monitoramento de múltiplos servidores (`www1`, `www2`, `mailsv`, etc.).

## 🛠️ Stack Tecnológica
- **OS:** Arch Linux (Kernel 6.x)
- **SIEM:** Wazuh 4.10.0
- **Containerização:** Docker & Docker Compose
- **Ferramentas:** Bash, XML Configuration, YAML.

## 🔧 Troubleshooting
Durante a implementação, resolvi os seguintes desafios técnicos:

1. **Gestão de Dependências no Arch:** Instalação manual do `unzip` via `pacman` para manipulação dos datasets brutos.
2. **Hierarquia XML Corrompida:** Recuperação do arquivo `ossec.conf` após falha de sintaxe nas tags `<localfile>`, garantindo a integridade do serviço `wazuh-logcollector`.
3. **Mapeamento de Volumes (Docker):** Sincronização de diretórios locais do Host com o sistema de arquivos do Container para persistência de dados.
4. **Globbing Recursivo:** Configuração de busca em subdiretórios utilizando o padrão `**/*.log`, permitindo que o Wazuh monitore pastas aninhadas automaticamente.

## 📊 Arquitetura de Dados
Os logs são extraídos no host e montados no container conforme o esquema:
`Host: ./dados/` -> `Container: /media/dados/ (ro)`

## 📈 Resultados
- Centralização de logs de acesso (HTTP) e segurança (SSH).
- Visualização de alertas históricos através da manipulação de filtros temporais no Dashboard do Wazuh.
- Monitoramento em tempo real de novos arquivos inseridos no diretório de dados.

---
*Projeto desenvolvido por Eric Andrey dos Santos como parte dos estudos de ADS e CyberSecurity.*

# Meu Projeto Wazuh

Aqui está o dashboard que configurei: 
![Wazuh Dashboard](/home/eran/wazuh-docker/single-node/screenshot.png)
