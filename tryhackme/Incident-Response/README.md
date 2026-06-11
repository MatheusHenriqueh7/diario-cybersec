O que é um Incidente?

Quando uma solução de segurança detecta eventos associados a uma possível atividade maliciosa, ela dispara um alerta. Esse alerta pode ser:

TipoDefiniçãoExemploFalso PositivoAlerta que parece perigoso mas não éBackup para nuvem disparando alerta de exfiltração de dadosVerdadeiro PositivoAlerta que aponta para algo realmente prejudicialE-mail de phishing confirmado pela equipe de segurança

Alertas verdadeiros positivos são chamados de incidentes. Todo incidente recebe um nível de gravidade: baixa, média, alta ou crítica — que define a ordem de prioridade de resposta.


Tipos de Incidentes

TipoO que éInfecção por MalwarePrograma malicioso que danifica sistemas. Principal causa: arquivos maliciosos (docs, executáveis, etc.)Violação de SegurançaAcesso não autorizado a dados confidenciaisVazamento de DadosExposição de informações confidenciais — pode ser intencional ou por erro humanoAtaque InternoAtaque originado dentro da própria organização (ex: funcionário insatisfeito)DoS (Negação de Serviço)Sobrecarga de um sistema com requisições falsas, tornando-o indisponível para usuários legítimos


A gravidade de cada incidente depende do contexto da organização — um DoS pode ser crítico para uma empresa que depende do site, mas irrelevante para outra.




Frameworks de Resposta a Incidentes

SANS — 6 fases (PICERL)

LetraFaseO que fazPPreparaçãoTreina equipe, cria planos e implanta ferramentas antes do incidenteIIdentificaçãoDetecta comportamento anormal — é aqui que SIEM, AV e EDR atuamCContençãoIsola a máquina infectada para o problema não se espalharEErradicaçãoRemove a ameaça do ambiente (ex: varredura de malware)RRecuperaçãoRestaura sistemas a partir de backup e coloca de volta em produçãoLLições AprendidasReunião pós-incidente — o que falhou? Como evitar da próxima vez?

NIST — 4 fases (versão condensada)

Fase NISTEquivalente SANSPreparaçãoPreparaçãoDetecção e AnáliseIdentificaçãoContenção, Erradicação e RecuperaçãoC + E + RAtividade Pós-IncidenteLições Aprendidas


Ferramentas de Detecção

FerramentaFunçãoSIEMCentraliza e correlaciona logs de toda a rede para identificar incidentesAV (Antivírus)Detecta malwares conhecidos e varre o sistema regularmenteEDRProtege endpoints contra ameaças avançadas e pode conter/erradicar ameaças automaticamente


Playbooks e Runbooks

Após identificar um incidente, seguir um processo padronizado economiza tempo e reduz erros.


Playbook — guia geral de resposta para cada tipo de incidente
Runbook — execução detalhada passo a passo de ações específicas durante o incidente


Exemplo de Playbook para Phishing:


Notificar as partes interessadas
Analisar cabeçalho e corpo do e-mail
Verificar e analisar anexos
Checar se alguém abriu os anexos
Isolar sistemas infectados da rede
Bloquear o remetente



Exercício Prático — Resposta a Incidente de Phishing

Neste lab, atuei como Analista SOC e respondi a um incidente de phishing seguindo o framework SANS.

Detalhes do Incidente

CampoRespostaRemetente maliciosoJeff Johnson (j.johnson@ppc.com)Vetor de ameaçaEmail attachmentDispositivos que baixaram o anexo3Dispositivos que executaram o arquivo1FlagTHM{My_First_Incident_Response}

Fases do SANS aplicadas no lab


I (Identificação) — Analisei o e-mail, identifiquei o remetente, o vetor e os dispositivos afetados
C (Contenção) — Isolei o sistema comprometido da rede


Por que a diferença entre "baixou" e "executou" importa?


3 dispositivos baixaram → estão em risco, o arquivo ainda pode ser executado
1 dispositivo executou → está comprometido, o malware já rodou


Na vida real isso define a prioridade: isola imediatamente quem executou, mas também limpa quem só baixou antes que alguém clique.


Principais Aprendizados


Nem todo alerta é um incidente — saber distinguir falso positivo de verdadeiro positivo é parte central do trabalho do analista SOC
O nível de gravidade define a ordem de resposta — crítico sempre primeiro
SANS e NIST são frameworks complementares — SANS é mais detalhado, NIST mais condensado
Playbooks e Runbooks existem para padronizar a resposta e evitar improvisos sob pressão
O vetor de ameaça (como o ataque chegou) é diferente do payload (a ameaça em si)
