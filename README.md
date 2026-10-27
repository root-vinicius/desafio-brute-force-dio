# Relatório de Estudo: Auditoria de Segurança e Prevenção contra Ataques de Força Bruta

Este repositório contém a documentação prática e teórica elaborada para o desafio do curso de Segurança da Informação na plataforma **DIO (Digital Innovation One)**.

---

## 🎯 Objetivo do Projeto
Demonstrar a compreensão teórica e prática sobre os conceitos de autenticação, testes de resistência de credenciais (*Brute Force* e *Password Spraying*) em ambientes controlados e isolados, e mapear as principais estratégias defensivas para mitigar esse tipo de vulnerabilidade.

---

## 🖥️ Topologia e Configuração do Laboratório
Para a realização dos estudos e simulações com segurança, utilizou-se um ambiente virtualizado totalmente isolado:

* **Gerenciador de Virtualização:** Oracle VM VirtualBox.
* **Modo de Rede:** Rede Interna / *Host-Only* (sem comunicação ou acesso à rede externa/Internet).
* **Máquina Atacante / Auditoria:** Kali Linux (contendo ferramentas como Medusa, Nmap e Smbclient).
* **Máquina Alvo / Vulnerável:** Metasploitable 2 e aplicação DVWA (*Damn Vulnerable Web Application*).

> **Nota de Segurança:** Todos os testes de verificação foram restritos ao ambiente de laboratório isolado, respeitando as boas práticas e diretrizes éticas da segurança da informação.

--- ![Evidência do IP do Metasploitable](foto.png)

## 🔍 Conceitos Estudados

### 1. Ataque de Força Bruta (*Brute Force*)
Consiste no teste exaustivo de combinações de usuários e senhas (frequentemente com o auxílio de dicionários ou *wordlists*) contra um serviço de autenticação (ex.: FTP, SSH, formulários Web).

### 2. Password Spraying
Técnica que visa burlar mecanismos de bloqueio de conta (*Account Lockout*). Em vez de tentar milhares de senhas para um único usuário, o testador tenta poucas senhas comuns (ex.: `Senha123`, `Mudar123`) contra uma vasta lista de contas válidas.

### 3. Ferramenta Medusa
Utilizada no Kali Linux para testes de autenticação paralelos e modulares em diversos protocolos de rede (como FTP, HTTP, SMB).

---

## 🛡️ Medidas de Prevenção e Mitigação (Segurança Defensiva)

Para proteger sistemas e aplicações contra tentativas de força bruta e *password spraying*, devem ser adotadas as seguintes defesas:

1. **Políticas de Senhas Fortes:** Exigir comprimento mínimo (ex.: 12+ caracteres) e diversidade de caracteres (letras maiúsculas, minúsculas, números e símbolos).
2. **Bloqueio de Conta (*Account Lockout Policy*):** Bloquear temporariamente a conta após um número limite de tentativas incorretas consecutivas.
3. **Limitação de Taxa (*Rate Limiting*):** Restringir a quantidade de requisições permitidas por IP em um determinado intervalo de tempo.
4. **Autenticação Multi-Fator (MFA / 2FA):** Exigir um segundo fator de confirmação (como aplicativo autenticador ou token físico), invalidadando o acesso apenas por senha.
5. **Uso de CAPTCHA:** Implementar desafios interativos em formulários de login para impedir a automação por scripts e bots.
6. **Monitoramento e Detecção:** Utilizar soluções como o Fail2ban ou sistemas SIEM para analisar logs do sistema (ex.: `/var/log/auth.log`) e bloquear IPs suspeitos automaticamente.

---

## 📚 Conclusão
O desafio permitiu compreender como funcionam as automações de testes de credenciais e reforçou a importância crucial de implementar múltiplas camadas de defesa (Defense in Depth) para garantir a integridade e confidencialidade dos sistemas corporativos.


Desafio: Simulação de Ataques de Força Bruta e Mitigação de RiscosEste repositório documenta a realização do laboratório prático de segurança da informação, focando na configuração de um ambiente virtualizado, testes de autenticação e análise de medidas defensivas.🛠️ Ambiente de LaboratórioSistema Anfitrião (Host): Fedora com GNOME Boxes.Máquina Atacante: Kali Linux.Máquina Alvo (Vulnerável): Metasploitable 2 (msfadmin/msfadmin).   📸 Evidências do Laboratório1. Inicialização e Identificação do Alvo (Metasploitable 2)Configuração e verificação do endereço IP privado da máquina alvo através do comando ifconfig:   Plaintexteth0      Link encap:Ethernet  HWaddr 52:54:00:29:40:47  
          
          inet addr:192.168.122.143  Bcast:192.168.122.255  Mask:255.255.255.0
  2. Análise de Conectividade e Isolamento de RedeDurante a fase de testes de integração na rede virtualizada do ambiente (GNOME Boxes), analisou-se o comportamento das interfaces de rede entre os nós, documentando o isolamento de rede e a importância de políticas de segmentação corretas.📖 Fundamentos TeóricosAtaques de Força Bruta (Brute Force)Um ataque de força bruta consiste na tentativa sistemática de adivinhar credenciais (nome de utilizador e password) testando exaustivamente combinações possíveis até encontrar a correta. Em ambientes vulneráveis como o Metasploitable 2, serviços expostos com credenciais padrão fracas tornam-se alvos fáceis para estas abordagens.Password SprayingAo contrário do ataque de força bruta tradicional (que testa muitas senhas num único utilizador), o Password Spraying testa uma única senha comum (ou um pequeno lote) contra vários nomes de utilizador diferentes. O objetivo é evitar bloqueios de conta automáticos que detetam múltiplas tentativas falhadas para a mesma conta.🛡️ Medidas de Mitigação e DefesaPara proteger sistemas contra este tipo de ataques, devem ser implementadas as seguintes práticas de segurança:Políticas de Senhas Fortes: Eliminar credenciais padrão (como msfadmin:msfadmin) e obrigar o uso de senhas complexas e longas.   Autenticação Multifator (MFA): Adicionar uma camada extra de verificação além da password tradicional.Bloqueio de Contas e Limitação de Taxa (Rate Limiting): Configurar políticas para bloquear temporariamente o IP ou a conta após um número limite de tentativas falhadas de login.Utilização de Firewalls e IDS/IPS: Monitorar e restringir o acesso a portas de serviços sensíveis (como SSH, FTP, Telnet) apenas a redes confiáveis.
