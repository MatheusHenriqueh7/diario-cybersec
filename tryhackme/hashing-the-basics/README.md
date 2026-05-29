# Noções Básicas de Hashing

## O que é Hash
Uma função hash recebe dados de qualquer tamanho e gera 
um código de tamanho fixo — como uma impressão digital 
única do arquivo ou senha.

## Propriedade mais importante — Efeito Avalanche
Qualquer mudança mínima na entrada gera um hash 
completamente diferente. Exemplo: T e U diferem por 
1 bit mas geram hashes totalmente diferentes.

## Formas inseguras de armazenar senhas
- Texto simples — expõe a senha diretamente
- Criptografia obsoleta — algoritmos fracos e quebráveis
- Hash inseguro — como MD5 e SHA-1, já considerados fracos

## Forma segura — Bcrypt
Armazena apenas o hash da senha, nunca a senha original.
Bcrypt é lento de propósito, dificultando ataques de força bruta.
Identificado pelo prefixo $2a$ no hash.

## Algoritmos

| Algoritmo | Tamanho | Segurança |
|---|---|---|
| MD5 | 32 caracteres | Fraco |
| SHA-1 | 40 caracteres | Fraco |
| SHA-256 | 64 caracteres | Forte |
| Bcrypt | Variável | Muito forte |

## Ferramentas utilizadas

### Gerar hash de arquivos
sha256sum arquivo.txt
Usado para verificar integridade — se o hash bater 
com o original, o arquivo não foi alterado.

### Quebrar hashes — Hashcat
hashcat -m 3200 -a 0 hash.txt rockyou.txt
Testa senhas de uma wordlist até encontrar a que 
gera o mesmo hash.

### Consultar hashes online — CrackStation
Site com banco de hashes já quebrados. Útil para 
hashes simples sem precisar do hashcat.

### Base64 — não é hash!
base64 -d arquivo.txt
Base64 é codificação reversível — diferente do hash 
que não tem volta.

## Na vida real
- Verificar se arquivos baixados são legítimos
- Identificar malware pelo hash no VirusTotal
- Provar integridade de evidências em forense digital
- Testar força de senhas de usuários
