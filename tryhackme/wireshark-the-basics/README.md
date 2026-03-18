# Wireshark: The Basics

## Objetivo da sala

Esta sala tem como objetivo introduzir o uso do Wireshark para análise de tráfego de rede, mostrando como inspecionar pacotes, aplicar filtros e interpretar dados transmitidos em protocolos como HTTP.

## Plataforma

- TryHackMe

## Ferramenta principal

- Wireshark

## Conceitos trabalhados

- captura de tráfego de rede
- análise de pacotes
- filtros no Wireshark
- protocolo HTTP
- diferença entre headers e body
- Follow HTTP Stream
- inspeção de conteúdo HTML
- extração de arquivos
- verificação de hash

## O que pratiquei

Durante esta sala, pratiquei a análise de tráfego HTTP dentro do Wireshark, observando como os pacotes trafegam e como localizar informações úteis dentro das respostas do servidor.

Também utilizei filtros para isolar pacotes relevantes e explorei o recurso **Follow HTTP Stream**, que facilita a visualização do conteúdo trocado entre cliente e servidor.

Além disso, aprendi a identificar dados presentes no corpo da resposta HTTP, especialmente conteúdo HTML, e percebi que muitas informações importantes não estão nos headers, mas sim no body da resposta.

## Técnicas utilizadas

- aplicação de filtro `http`
- inspeção de pacotes manualmente
- expansão de campos como line-based text data
- uso do recurso Follow HTTP Stream
- leitura de conteúdo HTML retornado pelo servidor
- busca por informações relevantes dentro da resposta
- análise de arquivos transferidos
- geração e conferência de hash MD5

## Principais aprendizados

Os principais aprendizados desta sala foram:

- entender melhor como o tráfego HTTP aparece no Wireshark
- diferenciar headers de body em uma resposta HTTP
- localizar informações úteis dentro do conteúdo HTML
- usar o Follow HTTP Stream como apoio na investigação
- desenvolver mais atenção na análise prática de pacotes

## Conclusão

Esta sala foi importante para consolidar conceitos introdutórios de análise de tráfego de rede e para ganhar familiaridade com o Wireshark na prática.

Ela também reforçou a importância de investigar com calma o conteúdo das respostas, interpretar os dados corretamente e usar os recursos da ferramenta para facilitar a análise.
