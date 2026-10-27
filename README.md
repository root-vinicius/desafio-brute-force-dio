# Relatório de Estudo: Auditoria de Segurança e Prevenção contra Ataques de Força Bruta

Este repositório contém a documentação prática e teórica elaborada para o desafio do curso de Segurança da Informação na plataforma **DIO (Digital Innovation One)**.

---

## 🎯 Objetivo do Projeto

Demonstrar a compreensão teórica e prática sobre os conceitos de autenticação, testes de resistência de credenciais (*Brute Force* e *Password Spraying*) em ambientes controlados e isolados, e mapear as principais estratégias defensivas para mitigar esse tipo de vulnerabilidade.

---

## 🖥️ Topologia e Configuração do Laboratório

- **Sistema Anfitrião (Host):** Fedora Linux com GNOME Boxes.
- **Máquina Atacante:** Kali Linux (Medusa, Nmap, enum4linux).
- **Máquina Alvo:** Metasploitable 2 e aplicação DVWA (*Damn Vulnerable Web Application*).
- **Modo de Rede:** Rede isolada/NAT do GNOME Boxes (sem acesso à internet a partir do alvo).

> **Nota de Segurança:** Todos os testes foram restritos a um ambiente de laboratório isolado, respeitando as boas práticas e diretrizes éticas da segurança da informação.

### Identificação do alvo (Metasploitable 2)

![Evidência do IP do Metasploitable](foto.png)

eth0 Link encap:Ethernet HWaddr 52:54:00:29:40:47
inet addr:192.168.122.143 Bcast:192.168.122.255 Mask:255.255.255.0


---

## 🔍 Conceitos Estudados

### 1. Ataque de Força Bruta (*Brute Force*)
Consiste no teste exaustivo de combinações de usuários e senhas (geralmente com wordlists) contra um serviço de autenticação, até encontrar a credencial correta.

### 2. Password Spraying
Técnica que inverte a lógica do brute force tradicional: em vez de testar muitas senhas para um único usuário, testa-se poucas senhas comuns contra uma lista ampla de usuários — evitando bloqueios de conta por tentativas repetidas no mesmo login.

### 3. Ferramenta Medusa
Ferramenta de autenticação paralela e modular, usada no Kali Linux para testes contra diversos protocolos de rede (FTP, HTTP, SMB, SSH, entre outros).

---

## 🧪 Execução dos Testes

### Wordlists utilizadas

Wordlists simples, criadas apenas para fins didáticos, disponíveis em `/wordlists`:

**usuarios.txt**

msfadmin
admin
root
user


**senhas.txt**

msfadmin
123456
password
admin
toor


### 1. Força Bruta em FTP

Comando utilizado:
```bash
medusa -h 192.168.122.143 -U wordlists/usuarios.txt -P wordlists/senhas.txt -M ftp
```

**Resultado:**
> _(cole aqui o print/resultado do terminal mostrando o login encontrado)_

### 2. Password Spraying em SMB com enumeração de usuários

Enumeração de usuários:
```bash
enum4linux -U 192.168.122.143
```

Password spraying:
```bash
medusa -h 192.168.122.143 -U wordlists/usuarios_enumerados.txt -p msfadmin -M smbnt
```

**Resultado:**
> _(cole aqui o print/resultado da enumeração e do spray)_

### 3. Automação de tentativas em formulário Web (DVWA)

- DVWA configurado com nível de segurança **Low**, para fins didáticos.
- Módulo de login acessado em `http://192.168.122.143/dvwa/login.php`.

Comando/método utilizado:
```bash
# (cole aqui o comando do Medusa com módulo web-form, ou a configuração usada no Burp Intruder)
```

**Resultado:**
> _(cole aqui o print/resultado do ataque ao formulário)_

---

## 🛡️ Medidas de Prevenção e Mitigação

1. **Políticas de Senhas Fortes:** eliminar credenciais padrão (como `msfadmin:msfadmin`) e exigir comprimento mínimo (12+ caracteres) com diversidade de tipos de caractere.
2. **Bloqueio de Conta (*Account Lockout*):** bloquear temporariamente a conta após um número limite de tentativas incorretas consecutivas.
3. **Limitação de Taxa (*Rate Limiting*):** restringir requisições por IP em um intervalo de tempo.
4. **Autenticação Multifator (MFA/2FA):** exigir um segundo fator além da senha.
5. **CAPTCHA:** em formulários web, para impedir automação por scripts e bots.
6. **Monitoramento e Detecção:** uso de Fail2ban ou SIEM para analisar logs (ex.: `/var/log/auth.log`) e bloquear IPs suspeitos automaticamente.
7. **Firewalls e IDS/IPS:** restringir acesso a portas sensíveis (SSH, FTP, SMB) apenas a redes confiáveis.

---

## 📚 Conclusão

O desafio permitiu compreender na prática como funcionam ataques de automação de credenciais contra diferentes serviços (FTP, SMB, aplicações web), reforçando a importância de múltiplas camadas de defesa (*Defense in Depth*) para proteger sistemas corporativos.
