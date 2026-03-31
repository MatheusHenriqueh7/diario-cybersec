# Noções Básicas de Tcpdump

## Objetivo da sala
Aprender a usar o tcpdump no Linux para 
filtrar e analisar pacotes de rede.

## O que é o tcpdump
Ferramenta de linha de comando no Linux 
que permite filtrar e analisar pacotes 
de rede de forma rápida e prática.

## Comandos aprendidos

| Comando | O que faz |
|---|---|
| `tcpdump -r arquivo.pcap` | Lê um arquivo de captura |
| `tcpdump -n` | Mostra IPs sem converter para nomes |
| `tcpdump -e` | Inclui endereços MAC no output |
| `tcpdump -q` | Output resumido |
| `tcpdump greater 15000` | Filtra pacotes maiores que X bytes |
| `comando \| wc -l` | Conta o número de pacotes |

## Protocolos filtrados
- **ICMP** — ping e mensagens de erro
- **ARP** — descoberta de endereços MAC
- **TCP** — conexões com flags SYN, ACK, RST
- **DNS** — consultas de nomes de domínio (UDP porta 53)

## O que aprendi na prática
- Filtrar pacotes por protocolo
- Contar pacotes automaticamente
- Identificar IP de origem usando `-n`
- Filtrar flags TCP específicas
- Encontrar pacotes por tamanho

## Por que isso importa
O tcpdump é essencial para análise de 
incidentes. Com ele é possível identificar 
comportamentos suspeitos na rede como 
port scans, ataques de reset e 
exfiltração de dados.

## Conclusão
Sem o tcpdump você fica sem uma das 
principais ferramentas de análise de 
tráfego. Ele permite investigar qualquer 
incidente de rede de forma rápida e eficaz.
