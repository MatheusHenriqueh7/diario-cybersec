# Noções Básicas de Nmap

## Objetivo da sala
Aprender a usar o Nmap para descobrir dispositivos 
ativos na rede, identificar serviços em execução 
e extrair informações sobre os alvos.

## O que é o Nmap
Scanner de rede que permite descobrir quais dispositivos 
estão conectados numa rede e quais serviços estão 
sendo executados em cada um deles.

## Comandos aprendidos

| Comando | O que faz | Quando usar |
|---|---|---|
| `nmap -sL` | Lista hosts sem escanear | Ver IPs de uma faixa |
| `nmap -sn` | Descobre hosts ativos sem escanear portas | Reconhecimento inicial |
| `nmap -sS` | SYN Scan — varredura silenciosa | Pentest discreto |
| `nmap -sT` | Connect Scan — handshake completo | Sem privilégios root |
| `nmap -sU` | Varredura UDP | Descobrir serviços UDP |
| `nmap -O` | Detecta sistema operacional | Identificar o alvo |
| `nmap -sV` | Detecta versão dos serviços | Encontrar vulnerabilidades |
| `nmap -A` | Detecção completa — SO + versão + scripts | Análise detalhada |
| `nmap -Pn` | Força varredura em hosts inativos | Host não responde ICMP |
| `nmap -f` | Varredura rápida — 100 portas comuns | Reconhecimento rápido |
| `nmap -v` | Verbose — mostra progresso | Acompanhar varredura |
| `nmap -T<0-5>` | Controle de velocidade | Ajustar velocidade/ruído |
| `nmap -oA` | Salva relatório nos 3 principais formatos | Documentar varredura |

## Tipos de varredura

### SYN Scan `-sS`
Não completa o Three-Way Handshake — mais silencioso 
e deixa menos rastros nos logs. Requer privilégios root.

Nmap → SYN      → Alvo
Nmap ← SYN+ACK  ← Alvo  ✅ porta aberta
Nmap → RST      → Alvo  (encerra sem completar)

### Connect Scan `-sT`
Completa o handshake inteiro — mais barulhento 
mas não precisa de privilégios root.

Nmap → SYN      → Alvo
Nmap ← SYN+ACK  ← Alvo  ✅ porta aberta
Nmap → ACK      → Alvo  (conexão completa)

## Sub-redes
O Nmap permite escanear faixas de IP inteiras:

| Máscara | Quantidade de IPs |
|---|---|
| `/24` | 256 IPs |
| `/27` | 32 IPs |
| `/28` | 16 IPs |

Exemplo:
```bash
nmap -sL 192.168.0.1/27
```

## Por que isso importa
O Nmap é a principal ferramenta de reconhecimento 
em pentest e análise de segurança. Com ele é possível:
- Mapear dispositivos ativos na rede
- Identificar serviços e versões vulneráveis
- Detectar sistemas operacionais dos alvos
- Encontrar portas abertas desnecessariamente

## Conclusão
Dominar o Nmap é essencial para qualquer analista 
de segurança. É a primeira ferramenta usada numa 
análise de rede, seja para defesa ou para pentest.
