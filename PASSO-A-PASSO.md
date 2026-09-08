# 🛠️ Documentação Técnica Passo a Passo: Homelab Active Directory & Infraestrutura de Redes

Esta documentação contém o passo a passo detalhado para a implementação de um ambiente corporativo virtualizado simulando a infraestrutura completa de uma empresa, utilizando **Windows Server 2022**, **Active Directory (AD DS)**, **DNS**, **DHCP**, **File Server (Permissões NTFS)**, **Group Policy (GPO)** e máquinas clientes com **Windows 11**.

---

## 📌 Sumário
1. [Configurações Iniciais das Máquinas Virtuais](#1-configurações-iniciais-das-máquinas-virtuais)
2. [Instalação e Configuração do Windows Server 2022](#2-instalação-e-configuração-do-windows-server-2022)
3. [Instalação e Promoção do Active Directory (AD DS)](#3-instalação-e-promoção-do-active-directory-ad-ds)
4. [Criação de Unidades Organizacionais (OUs) e Primeiros Usuários](#4-criação-de-unidades-organizacionais-ous-e-primeiros-usuários)
5. [Instalação e Configuração do Servidor DHCP](#5-instalação-e-configuração-do-servidor-dhcp)
6. [Criação e Configuração da Máquina Cliente (PC01 - Windows 11)](#6-criação-e-configuração-da-máquina-cliente-pc01---windows-11)
7. [Ingresso da Máquina Cliente no Domínio](#7-ingresso-da-máquina-cliente-no-domínio)
8. [Gerenciamento de Grupos de Segurança e Permissões](#8-gerenciamento-de-grupos-de-segurança-e-permissões)
9. [Implementação e Compartilhamento do File Server (Permissões NTFS)](#9-implementação-e-compartilhamento-do-file-server-permissões-ntfs)
10. [Troubleshooting e Validação de Tokens de Segurança Kerberos](#10-troubleshooting-e-validação-de-tokens-de-segurança-kerberos)
11. [Implementação de Políticas de Grupo (GPO - Política de Senhas)](#11-implementação-de-políticas-de-grupo-gpo---política-de-senhas)
12. [Reestruturação Profissional de OUs e Cadastro de Usuários](#12-reestruturação-profissional-de-ous-e-cadastro-de-usuários)
13. [Automação com GPO: Mapeamento de Unidades de Rede (Disco Z:)](#13-automação-com-gpo-mapeamento-de-unidades-de-rede-disco-z)

---

## 1. Configurações Iniciais das Máquinas Virtuais

### Etapa 01: Criação da VM do Controlador de Domínio (`DC01`)
Após a instalação do Oracle VM VirtualBox, download das imagens ISO oficiais do **Windows Server 2022** e **Windows 11**, e a habilitação da virtualização de hardware no processador, foram realizadas as configurações iniciais da máquina virtual principal:

* **Nome da VM:** `DC01`
* **Memória RAM:** 4096 MB (4 GB)
* **Processadores:** 2 vCPUs
* **Disco Rígido:** 40 GB (VDI)
* **ISO Carregada:** Windows Server 2022 Datacenter Evaluation

<img width="945" height="723" alt="1Parte 1 - Configurações Iniciais 1" src="https://github.com/user-attachments/assets/3364b0dc-0b0b-449e-91c4-83656a0706b7" />


---

### Etapa 02: Resumo da Configuração no VirtualBox
Validação do sumário de configurações da VM `DC01` antes da primeira inicialização do sistema operacional.

<img width="1919" height="1029" alt="2Parte 1 - Configurações iniciais 2" src="https://github.com/user-attachments/assets/c0a8c3e5-1366-4595-b573-129cb88a36e6" />


---

### Etapa 03: Isolamento de Rede Virtual (Rede Interna)
Para garantir a segurança do ambiente e evitar que o servidor DHCP do laboratório interfira na rede física residencial/corporativa:

* **Modo de Rede:** Alterado de `NAT` para `Rede Interna` (*Internal Network*).
* **Nome da Rede:** Definido como `LAB_REDE`.

<img width="1919" height="1027" alt="3Parte 2 - Configurando a rede" src="https://github.com/user-attachments/assets/e1d34d64-b26d-4f49-bef7-9d4b57cd7d56" />


---

## 2. Instalação e Configuração do Windows Server 2022

### Etapa 04: Seleção da Edição e Instalação
Durante o assistente de instalação do Windows Server:
* **Edição Selecionada:** `Windows Server 2022 Datacenter Evaluation (Desktop Experience)`.
  > *Nota:* A opção *Desktop Experience* foi escolhida para fornecer a interface gráfica de usuário (GUI). A opção sem essa marcação instala a versão *Server Core* (operada estritamente via linha de comando).
* **Configuração de Conta:** Definição da senha de Administrador local do servidor.

<img width="624" height="471" alt="4Parte 3 - Instalando o Windows Server 2022" src="https://github.com/user-attachments/assets/adaf85ec-267a-430e-81f3-ca4bcf3dbfd7" />



---

### Etapa 05: Definindo Nome e Descrição da Máquina
No **Server Manager** (Gerenciador do Servidor), foram configuradas as informações de identificação do computador:

* **Nome do Computador:** `DC01`
* **Descrição do Computador:** `Lab Server`

<img width="1920" height="1009" alt="5Parte 4 - Server Manager" src="https://github.com/user-attachments/assets/e68404bd-3108-4b6f-ba59-261b3bf988b3" />

---

### Etapa 06: Configuração de Endereço IP Estático
Para garantir o funcionamento estável dos serviços de rede corporativos (DNS/AD DS), o servidor deve obrigatoriamente possuir um IP estático:

* **Endereço IP:** `192.168.10.1`
* **Máscara de Sub-rede:** `255.255.255.0`
* **Gateway Padrão:** *Em branco (Ambiente isolado)*
* **Servidor DNS Preferencial:** `127.0.0.1` (Apontando para a própria máquina)

<img width="1920" height="1009" alt="6Parte  4 - Server Manager 2" src="https://github.com/user-attachments/assets/4f1f2857-44ce-4025-a6e5-1afe9ace6b3c" />

---

## 3. Instalação e Promoção do Active Directory (AD DS)

### Etapa 07: Adicionando a Função AD DS
No **Server Manager**, navegou-se até `Manage` > `Add Roles and Features`:
* Na aba **Server Roles**, marcou-se a opção **Active Directory Domain Services**.
* Na janela pop-up referente aos recursos dependentes, confirmou-se clicando em **Add Features**.

<img width="1920" height="1009" alt="7Parte 5 - Active Directory" src="https://github.com/user-attachments/assets/c9fc4d7f-c8ef-4fd0-be12-e3220a029c78" />


---

### Etapa 08: Conclusão da Instalação das Funções
Tela de confirmação do término do download e instalação das ferramentas do Active Directory no servidor.

<img width="1920" height="1009" alt="8Parte 5 - Active Directory 2" src="https://github.com/user-attachments/assets/369041b1-29de-4b58-a34c-2c46ea552cfa" />


---

### Etapa 09: Promoção a Controlador de Domínio (Nova Floresta)
Após a instalação das funções, iniciou-se o assistente de promoção do servidor (*Promote this server to a domain controller*):

* **Operação de Implantação:** Selecionado `Add a new forest` (Adicionar uma nova floresta).
* **Nome do Domínio Raiz (*Root domain name*):** `lab.local`

<img width="1920" height="1009" alt="9Parte 6 - Promoção do Servidor 1" src="https://github.com/user-attachments/assets/0b411b19-8335-4233-83d4-603702efb603" />


---

### Etapa 10: Opções do Controlador de Domínio e DSRM
* **Nível Funcional da Floresta/Domínio:** Mantido em `Windows Server 2016` (padrão).
* **Senha DSRM:** Definição de uma senha forte para o Modo de Restauração dos Serviços de Diretório.

<img width="1920" height="1009" alt="10Parte 6 - Promoção do Servidor 2" src="https://github.com/user-attachments/assets/6eef5d06-81e6-4830-9344-211ba26c0447" />


---

### Etapa 11: Opções de DNS (Aviso de Delegação)
Na tela de opções de DNS, o aviso amarelo *"A delegation for this DNS server cannot be created..."* foi exibido. 
> *Nota:* Este aviso é normal e esperado em um ambiente isolado, pois este é o primeiro e único servidor DNS autoritativo da zona raiz. A mensagem foi ignorada e avançou-se em **Next**.

<img width="1920" height="1009" alt="11Parte 6 - Promoção do Servidor 3" src="https://github.com/user-attachments/assets/4c9fcb71-085e-4123-a17c-82abd138dfa3" />


---

### Etapa 12: Opções Adicionais (NetBIOS e Caminhos)
* **Nome NetBIOS:** Confirmado como `LAB`.
* **Caminhos de Banco de Dados/Logs (SYSVOL):** Mantidos nos diretórios padrão do sistema.

<img width="1920" height="1009" alt="12Parte 6 - Promoção do Servidor 4" src="https://github.com/user-attachments/assets/97665b0b-f50d-4b00-8723-3a66982f17e5" />


---

### Etapa 13: Verificação de Pré-requisitos e Instalação
O assistente executou a validação de pré-requisitos. Após a confirmação da mensagem verde *"All prerequisite checks passed successfully"*, clicou-se em **Install**. O servidor foi reiniciado automaticamente após o término.

<img width="1920" height="1009" alt="13Parte 6 - Promoção do Servidor 5" src="https://github.com/user-attachments/assets/272bb941-0ac7-497f-9086-4ec3f68ba306" />


---

## 4. Criação de Unidades Organizacionais (OUs) e Primeiros Usuários

### Etapa 14: Criação da Unidade Organizacional Principal
Abertura do **Active Directory Users and Computers** (`dsa.msc`):
1. Clique com botão direito sobre o domínio `lab.local` > `New` > `Organizational Unit`.
2. **Nome da OU:** `LAB_Empresa`.
3. Garantida a marcação da opção *"Protect container from accidental deletion"* (Proteger contra exclusão acidental).

<img width="1920" height="1009" alt="14Parte 7 - Unidade Organizacional 1" src="https://github.com/user-attachments/assets/1134a482-50b6-49b8-9be8-6ca681d6f77a" />


---

### Etapa 15: Estruturação de Sub-OUs e Cadastro do Primeiro Usuário
Dentro da OU `LAB_Empresa`, foram criadas duas sub-pastas:
* `Usuários`
* `Computadores`

Em seguida, na sub-pasta `Usuários`, criou-se o primeiro objeto do tipo Usuário:
* **First Name:** Mario | **Last Name:** Silva
* **User logon name:** `mario.silva` (`mario.silva@lab.local`)

<img width="1920" height="1009" alt="15Parte 7 - Unidade Organizacional 2" src="https://github.com/user-attachments/assets/2a6e0b13-8d9e-4668-b2aa-98d2edfcfd61" />


---

### Etapa 16: Definição de Credenciais e Regras do Usuário
* Definição de senha inicial forte.
* **Desmarcado:** *User must change password at next logon*.
* **Marcado:** *Password never expires* (Apenas para otimização das rotinas do laboratório).

<img width="1920" height="1009" alt="16Parte 7 - Unidade Organizacional 3" src="https://github.com/user-attachments/assets/9caf7a57-c3a1-4652-9f80-f0d21122872b" />

---

## 5. Instalação e Configuração do Servidor DHCP

### Etapa 17: Instalação da Função Servidor DHCP
No **Server Manager** > `Manage` > `Add Roles and Features`:
* Marcada a caixa **DHCP Server**.
* Confirmada a adição dos recursos adicionais de gerenciamento (*Add Features*).

<img width="1920" height="1009" alt="17Parte 8 - Instalando a Função de Servidor DHCP 1" src="https://github.com/user-attachments/assets/d31c09f5-e002-4e72-ae1e-3e68ebf96b2a" />


---

### Etapa 18: Finalização da Instalação do DHCP
Acompanhamento da barra de progresso e conclusão da instalação das ferramentas do DHCP.

<img width="1920" height="1009" alt="18Parte 8 - Instalando a Função de Servidor DHCP 2" src="https://github.com/user-attachments/assets/8e27a2b7-f05a-42e2-961d-d1ce128d5c2c" />


---

### Etapa 19: Autorização do DHCP no Active Directory (Notificação)
No topo do Server Manager, clicou-se no ícone da bandeira amarela de alerta e em **Complete DHCP configuration** para vincular o serviço ao AD.

<img width="1920" height="1009" alt="19Parte 9 - Autorizando o DHCP no Active Directory 1" src="https://github.com/user-attachments/assets/902d602a-9f4e-42c8-b066-814bc3b50012" />


---

### Etapa 20: Assistente de Autorização do DHCP
* **Credenciais Utilizadas:** `LAB\Administrator`.
* Finalização da autorização garantindo o status **Done** nas etapas de criação de grupos de segurança e autorização no controlador de domínio.

<img width="1920" height="1009" alt="20Parte 9 - Autorizando o DHCP no Active Directory 2" src="https://github.com/user-attachments/assets/808c9aa5-1075-42a4-9c78-736dd489d8b7" />


---

### Etapa 21: Criação do Escopo de Distribuição de IPs (*DHCP Scope*)
No console de gerenciamento do DHCP (`Tools` > `DHCP`):
1. Expandido o servidor `dc01.lab.local` > Clique com botão direito em `IPv4` > **New Scope...**
2. **Nome do Escopo:** `LAB_SCOPE`.

<img width="1920" height="1009" alt="21Parte 10 - Criando o Escopo de IPs (DHCP Scope)" src="https://github.com/user-attachments/assets/84185f94-0162-47e9-9a5e-635707602018" />


---

### Etapa 22: Definindo a Faixa de Endereços IP
Configuração do intervalo dinâmico de IPs que serão atribuídos às máquinas clientes:

* **Start IP Address:** `192.168.10.100`
* **End IP Address:** `192.168.10.200`
* **Length:** `24`
* **Subnet Mask:** `255.255.255.0`

<img width="1920" height="1009" alt="22Parte 10 - Criando o Escopo de IPs (DHCP Scope) 2" src="https://github.com/user-attachments/assets/7b15595d-9c9e-49cb-8750-21c5cd5222bf" />


---

### Etapa 23: Exclusões, Duração de Concessão e Opções de DNS
* **Exclusões de IP:** Nenhuma exclusão necessária dentro do bloco 100-200.
* **Lease Duration:** Mantido o padrão de 8 dias.
* **Parent Domain:** `lab.local`
* **DNS Server IP:** `192.168.10.1`

> *Nota:* Ao adicionar o IP `192.168.10.1`, o assistente exibe o alerta *"The IP Address is not a valid DNS address..."*. Isso ocorre porque o servidor está em rede isolada sem internet e a consulta de teste falha. Selecionou-se **Yes** para confirmar a inclusão.

<img width="1920" height="1009" alt="23Parte 10 - Criando o Escopo de IPs (DHCP Scope) 3" src="https://github.com/user-attachments/assets/42550c77-f570-48ae-863b-9cbdbd676e1f" />


---

### Etapa 24: Limpeza de Entradas e Ativação do Escopo
* Removido qualquer IP residual (ex.: `192.168.0.1`), deixando exclusivamente o IP `192.168.10.1`.
* **WINS Servers:** Mantido em branco.
* Finalizada a configuração marcando a opção de **Ativar o escopo imediatamente**.

<img width="1920" height="1009" alt="24Parte 10 - Criando o Escopo de IPs (DHCP Scope) 4" src="https://github.com/user-attachments/assets/6ea8d8a9-0f03-48d2-9295-a4d5987ce19c" />


---

## 6. Criação e Configuração da Máquina Cliente (PC01 - Windows 11)

### Etapa 25: Criação da VM do Cliente Windows 11
Criação da máquina virtual no VirtualBox para o sistema operacional cliente:

* **Nome da VM:** `PC01`
* **Desmarcada a opção:** *Proceed with Unattended Installation* (Instalação Não Atendida).
  > *Motivo:* A instalação automatizada do VirtualBox no Windows 11 pode criar usuários genéricos (`vboxuser`) ou causar travamentos em loop na tela OOBE. A instalação manual garante o controle total da criação da conta local temporária.

<img width="784" height="527" alt="25Parte 11 - Criação da Máquina Cliente" src="https://github.com/user-attachments/assets/4a36da4f-e5c4-4271-86d9-5c6f8d3c79af" />


---

### Etapa 26: Ajuste da Placa de Rede da VM Cliente
Antes de ligar o `PC01`, configurou-se a placa de rede para o mesmo segmento virtual do servidor:

* **Ligado a:** `Rede Interna`
* **Nome:** `LAB_REDE`

<img width="901" height="486" alt="26Parte 12 - Configurando a Rede da Máquina Cliente" src="https://github.com/user-attachments/assets/0af35cc7-ef3b-4e73-a8db-11a3960e36d8" />


---

## 7. Ingresso da Máquina Cliente no Domínio

### Etapa 27: Verificação Inicial de IP no Cliente
No `PC01`, abriu-se o Prompt de Comando (`cmd`) para checar as tabelas de rede via comando:
```cmd
ipconfig /all


