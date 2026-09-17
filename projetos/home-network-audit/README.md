Auditoria de Segurança — Rede Doméstica

Objetivo: mapear todos os dispositivos ativos na minha rede doméstica, identificar portas e serviços expostos, e avaliar riscos reais usando Nmap/Zenmap.

Ferramentas: Nmap 7.99 / Zenmap (Windows) Rede analisada: 192.168.1.0/24

Metodologia
1. Descoberta de hosts — primeira tentativa (ping scan)

Comecei com um scan simples de descoberta:

nmap -sn 192.168.1.0/24

Perfil "Ping scan" no Zenmap.

Resultado inesperado: apenas 2 hosts detectados — o roteador e meu próprio PC. Sabia que havia pelo menos mais 2 dispositivos ativos na rede (celulares), então parti para diagnosticar o motivo.

2. Diagnóstico do problema de descoberta

Investiguei três hipóteses possíveis, na ordem:

Privilégio insuficiente: reabri o Zenmap como Administrador. Sem mudança.
Sub-rede diferente (banda 2.4GHz vs 5GHz): conferi o IP do celular manualmente nas configurações de Wi-Fi — estava na mesma faixa (192.168.1.x), então essa hipótese foi descartada.
Isolamento de cliente (AP/Client Isolation) ou firewall descartando ICMP: essa se confirmou como a causa real.
3. Descoberta de hosts — segunda tentativa (ARP scan)

Troquei o método de descoberta de ping (ICMP) para ARP, mais confiável em redes locais:

nmap -PR -sn 192.168.1.0/24

Resultado: os 4 dispositivos da rede apareceram corretamente:

Dispositivo	IP	Fabricante
Roteador (Zyxel)	192.168.1.1	Zyxel Communications
Android (A56 de Maria)	192.168.1.165	—
iPhone (MatheusHenrique)	192.168.1.182	Apple
PC (DESKTOP-NOVO)	192.168.1.35	— (via Ethernet)

Lição: em redes domésticas modernas, nem todo dispositivo responde a ping ICMP simples — ARP é mais confiável para descoberta em LAN.

Scan de portas e serviços — Roteador (192.168.1.1)

Comando utilizado:

nmap -sV -A 192.168.1.1
Resultado
Porta	Serviço	Versão	Estado
21	FTP	—	filtered
22	SSH	—	filtered
23	Telnet	—	filtered
53	DNS	dnsmasq 2.67	open
80	HTTP	—	filtered
161	SNMP	não identificado	open
2601	Zebra (Quagga)	roteamento	open
8089	desconhecido	—	filtered
49152	UPnP	Portable SDK for UPnP devices 1.6.18	open

Sistema operacional identificado: Linux kernel 3.18.21 (via fingerprint TCP/IP)

Análise de risco

🔴 Achado principal — UPnP desatualizado (porta 49152) A versão identificada (Portable SDK for UPnP devices 1.6.18) corresponde à mesma biblioteca (libupnp) associada às vulnerabilidades divulgadas publicamente em 2012/2013 (CVE-2012-5958/5959), que na época afetaram milhões de dispositivos residenciais no mundo todo, segundo estudo da Rapid7. Trata-se do achado mais forte da auditoria, por ter CVE documentada associável à versão específica encontrada.

🟡 DNS desatualizado (porta 53 — dnsmasq 2.67) Versão de 2013, bem anterior às correções de segurança presentes em versões 2.78+ (conjunto de vulnerabilidades conhecido como "DNSpooq").

🟡 SNMP exposto (porta 161) Serviço aberto sem identificação de versão. SNMP mal configurado (community string padrão "public") é vetor comum de vazamento de configuração de roteador.

🟠 Zebra/Quagga exposto (porta 2601) Interface de configuração de roteamento. Roteadores de operadora historicamente já apresentaram esse serviço sem autenticação adequada, permitindo reconfiguração indevida.

🟢 Portas de administração filtradas (21, 22, 23, 80, 8089) Aparecem como "filtered", não abertas — o firewall do roteador está bloqueando acesso externo a esses serviços de administração, o que é uma postura positiva.

Verificação adicional (enumeração segura)

Tentei extrair mais informações do serviço UPnP via script NSE, sem risco de exploração:

nmap --script=upnp-info -p 49152 192.168.1.1

Não retornou detalhes adicionais (provavelmente resposta não-padrão do dispositivo), mas a versão já identificada no scan anterior foi suficiente para o achado.

Scan de portas — Dispositivos móveis
Android (192.168.1.165)
nmap -sV -PR -T4 --host-timeout 30s 192.168.1.165

Resultado: nenhuma porta respondeu — mesmo com host confirmado ativo via ARP, o scan de portas atingiu timeout sem retorno algum.

Interpretação: postura defensiva do dispositivo — firewall próprio descartando silenciosamente qualquer tentativa de conexão, sem expor nenhum serviço na rede local.

iPhone (192.168.1.182)
nmap -sV -PR -T4 --host-timeout 30s 192.168.1.182

Resultado:

Porta	Estado	Observação
49152	open (tcpwrapped)	Porta dinâmica/efêmera (faixa IANA), provavelmente associada a serviço Bonjour/Continuity da Apple
62078	open (tcpwrapped)	Documentada publicamente como porta do serviço lockdownd, usado para sincronização via iTunes/Finder

Interpretação: ambas as portas correspondem a serviços legítimos do ecossistema Apple, não configurações inseguras. Nenhuma delas representa vulnerabilidade — o achado aqui é a capacidade de diferenciar exposição de serviço legítimo de risco real, que é justamente a habilidade que importa em uma triagem de segurança.

Resumo geral
Dispositivo	Portas expostas	Nível de risco
Roteador (Zyxel)	DNS, SNMP, Zebra, UPnP	Alto (versões desatualizadas com CVEs conhecidas)
Android	Nenhuma	Baixo (bem protegido)
iPhone	2 (serviços legítimos Apple)	Baixo
PC (Windows)	Não escaneado nesta rodada	—
Recomendações
Atualizar firmware do roteador, se disponível pelo fabricante/operadora, para corrigir dnsmasq e UPnP desatualizados.
Desativar UPnP se não for estritamente necessário — é a exposição de maior risco encontrada.
Restringir ou desativar SNMP se não estiver em uso ativo para gerenciamento.
Verificar autenticação da interface Zebra/Quagga (porta 2601) — confirmar que não está acessível sem senha.
Lições aprendidas
Ping (ICMP) não é confiável para descoberta de hosts em redes domésticas modernas — ARP scan (-PR) é mais consistente em LAN.
Uma versão de software desatualizada, por si só, já é um indicador de risco válido para investigação — não é necessário "explorar" a vulnerabilidade para documentá-la como achado legítimo.
Nem toda porta aberta é uma falha: reconhecer serviços legítimos do sistema operacional (como os do iPhone) é parte essencial de uma triagem de segurança correta, evitando falsos positivos no relatório.
