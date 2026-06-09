Introduction to SOC
Plataforma: TryHackMe
Trilha: Cyber Security 101
Status: ✅ Concluída
Data: Junho 2026

O que é um SOC?
Um Security Operations Center (SOC) é uma equipe dedicada dentro de uma organização responsável por monitorar, detectar, analisar e responder continuamente a incidentes e ameaças de segurança.
O objetivo principal do SOC é garantir que qualquer atividade suspeita ou evento de segurança seja identificado e tratado antes de causar danos sérios à organização.

Níveis de Analistas do SOC
O SOC opera com uma estrutura hierárquica, onde os incidentes são escalados conforme a complexidade e severidade:
NívelFunçãoResponsabilidadesNível 1Analista de TriagemPrimeira linha de defesa. Monitora alertas, realiza triagem inicial e escala achados suspeitos para o N2Nível 2Respondedor de IncidentesInvestiga incidentes escalados em profundidade e trata casos de complexidade médiaNível 3Threat HunterCaça proativamente ameaças ainda não detectadas. Trata incidentes críticos e complexosSOC ManagerGestor da EquipeGerencia a equipe, processos e reporta para a liderança da organização

Ferramentas Principais do SOC
SIEM (Security Information and Event Management)
O hub central do SOC. Agrega logs de múltiplas fontes em toda a rede (firewalls, servidores, endpoints) e correlaciona eventos para identificar incidentes em escala.

Analogia: o SIEM é a central de segurança que monitora todas as câmeras do prédio ao mesmo tempo.

EDR (Endpoint Detection and Response)
Foca especificamente nos endpoints — computadores, laptops e servidores. Monitora o comportamento local da máquina em busca de processos suspeitos, arquivos maliciosos e ações não autorizadas.

Analogia: o EDR é a câmera individual dentro de uma sala específica.

Sistema de Tickets
Usado para abrir, rastrear e gerenciar casos de segurança após a detecção de um incidente. Exemplos: ServiceNow, Jira.

Exercício Prático — Investigação de Alerta no SIEM
Nesta sala, atuei como Analista SOC Nível 1 e investiguei um alerta real dentro de uma simulação de SIEM.
Alerta #167 — Port Scanning Activity Detected from IP: 10.0.0.8
Investigação utilizando o framework dos 5 W's:
WPerguntaRespostaWhat (O quê)Atividade que desencadeou o alertaPort ScanWhen (Quando)Horário da atividade12 de Junho de 2024 — 17:24Where (Onde)IP do host de destino10.0.0.3 (JOE PC)Who (Quem)IP do host de origem10.0.0.8 (NESSUS)Why (Por quê)Alguma resposta foi enviada de volta ao scanner?Sim — JOE PC respondeu para NESSUS, confirmando portas abertas
Principais observações dos logs

4.300 registros de log foram gerados entre 09:25 e 14:25 do dia 12 de Junho de 2024
A origem 10.0.0.8 (NESSUS) enviou tráfego para múltiplas portas de destino em rápida sucessão: 443, 53, 22, 21, 25, 80, 143 — padrão clássico de varredura de portas
Um registro de log mostrou 10.0.0.3 respondendo de volta para 10.0.0.8, confirmando que ao menos uma porta estava aberta
A porta 22 (SSH) respondeu — informação valiosa para um potencial atacante

Por que uma resposta importa?
Quando uma varredura de portas recebe resposta, significa que a porta está aberta e um serviço está rodando. Um atacante pode então mirar especificamente naquele serviço. Se nenhuma porta respondesse, o scanner não teria informação útil para agir.

Principais Aprendizados

O SOC opera 24/7 para detectar e responder a ameaças antes que causem danos
Analistas de Nível 1 são os primeiros a triar cada alerta — a maior parte do volume cai aqui
O framework dos 5 W's (O quê, Quando, Onde, Quem, Por quê) é uma forma estruturada de investigar qualquer alerta de segurança
SIEM e EDR se complementam: o SIEM enxerga o panorama geral da rede, o EDR enxerga fundo nas máquinas individuais
Mesmo uma ferramenta "legítima" como o Nessus (scanner de vulnerabilidades) gera alertas — o contexto é tudo na triagem


Referências

TryHackMe — Introduction to SOC
