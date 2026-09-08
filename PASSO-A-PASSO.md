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

![Configuração Inicial da VM DC01 no VirtualBox]<img width="945" height="723" alt="1Parte 1 - Configurações Iniciais 1" src="https://github.com/user-attachments/assets/c3783365-6e4e-4f19-ac2f-8fdb2145ee45" />


---

### Etapa 02: Resumo da Configuração no VirtualBox
Validação do sumário de configurações da VM `DC01` antes da primeira inicialização do sistema operacional.

![Resumo da VM no VirtualBox](<img width="1919" height="1029" alt="2Parte 1 - Configurações iniciais 2" src="https://github.com/user-attachments/assets/0817e97d-6bc1-4bda-bad1-fc5485366175" />
)

---

### Etapa 03: Isolamento de Rede Virtual (Rede Interna)
Para garantir a segurança do ambiente e evitar que o servidor DHCP do laboratório interfira na rede física residencial/corporativa:

* **Modo de Rede:** Alterado de `NAT` para `Rede Interna` (*Internal Network*).
* **Nome da Rede:** Definido como `LAB_REDE`.

![Configuração da Rede Interna no VirtualBox](caminho_da_imagem_aqui)

---

## 2. Instalação e Configuração do Windows Server 2022

### Etapa 04: Seleção da Edição e Instalação
Durante o assistente de instalação do Windows Server:
* **Edição Selecionada:** `Windows Server 2022 Datacenter Evaluation (Desktop Experience)`.
  > *Nota:* A opção *Desktop Experience* foi escolhida para fornecer a interface gráfica de usuário (GUI). A opção sem essa marcação instala a versão *Server Core* (operada estritamente via linha de comando).
* **Configuração de Conta:** Definição da senha de Administrador local do servidor.

![Seleção da ISO Windows Server Desktop Experience](caminho_da_imagem_aqui)

---

### Etapa 05: Definindo Nome e Descrição da Máquina
No **Server Manager** (Gerenciador do Servidor), foram configuradas as informações de identificação do computador:

* **Nome do Computador:** `DC01`
* **Descrição do Computador:** `Lab Server`

![Configuração de Nome do Servidor no Server Manager](caminho_da_imagem_aqui)

---

### Etapa 06: Configuração de Endereço IP Estático
Para garantir o funcionamento estável dos serviços de rede corporativos (DNS/AD DS), o servidor deve obrigatoriamente possuir um IP estático:

* **Endereço IP:** `192.168.10.1`
* **Máscara de Sub-rede:** `255.255.255.0`
* **Gateway Padrão:** *Em branco (Ambiente isolado)*
* **Servidor DNS Preferencial:** `127.0.0.1` (Apontando para a própria máquina)

![Configuração do IP Estático no Windows Server](caminho_da_imagem_aqui)

---

## 3. Instalação e Promoção do Active Directory (AD DS)

### Etapa 07: Adicionando a Função AD DS
No **Server Manager**, navegou-se até `Manage` > `Add Roles and Features`:
* Na aba **Server Roles**, marcou-se a opção **Active Directory Domain Services**.
* Na janela pop-up referente aos recursos dependentes, confirmou-se clicando em **Add Features**.

![Instalação da Função AD DS](caminho_da_imagem_aqui)

---

### Etapa 08: Conclusão da Instalação das Funções
Tela de confirmação do término do download e instalação das ferramentas do Active Directory no servidor.

![Conclusão da Instalação do AD DS](caminho_da_imagem_aqui)

---

### Etapa 09: Promoção a Controlador de Domínio (Nova Floresta)
Após a instalação das funções, iniciou-se o assistente de promoção do servidor (*Promote this server to a domain controller*):

* **Operação de Implantação:** Selecionado `Add a new forest` (Adicionar uma nova floresta).
* **Nome do Domínio Raiz (*Root domain name*):** `lab.local`

![Promoção do Servidor - Nova Floresta](caminho_da_imagem_aqui)

---

### Etapa 10: Opções do Controlador de Domínio e DSRM
* **Nível Funcional da Floresta/Domínio:** Mantido em `Windows Server 2016` (padrão).
* **Senha DSRM:** Definição de uma senha forte para o Modo de Restauração dos Serviços de Diretório.

![Opções do Controlador de Domínio e Senha DSRM](caminho_da_imagem_aqui)

---

### Etapa 11: Opções de DNS (Aviso de Delegação)
Na tela de opções de DNS, o aviso amarelo *"A delegation for this DNS server cannot be created..."* foi exibido. 
> *Nota:* Este aviso é normal e esperado em um ambiente isolado, pois este é o primeiro e único servidor DNS autoritativo da zona raiz. A mensagem foi ignorada e avançou-se em **Next**.

![Aviso de Delegação de DNS](caminho_da_imagem_aqui)

---

### Etapa 12: Opções Adicionais (NetBIOS e Caminhos)
* **Nome NetBIOS:** Confirmado como `LAB`.
* **Caminhos de Banco de Dados/Logs (SYSVOL):** Mantidos nos diretórios padrão do sistema.

![Configuração de Nome NetBIOS](caminho_da_imagem_aqui)

---

### Etapa 13: Verificação de Pré-requisitos e Instalação
O assistente executou a validação de pré-requisitos. Após a confirmação da mensagem verde *"All prerequisite checks passed successfully"*, clicou-se em **Install**. O servidor foi reiniciado automaticamente após o término.

![Verificação de Pré-requisitos com Sucesso](caminho_da_imagem_aqui)

---

## 4. Criação de Unidades Organizacionais (OUs) e Primeiros Usuários

### Etapa 14: Criação da Unidade Organizacional Principal
Abertura do **Active Directory Users and Computers** (`dsa.msc`):
1. Clique com botão direito sobre o domínio `lab.local` > `New` > `Organizational Unit`.
2. **Nome da OU:** `LAB_Empresa`.
3. Garantida a marcação da opção *"Protect container from accidental deletion"* (Proteger contra exclusão acidental).

![Criação da OU LAB_Empresa](caminho_da_imagem_aqui)

---

### Etapa 15: Estruturação de Sub-OUs e Cadastro do Primeiro Usuário
Dentro da OU `LAB_Empresa`, foram criadas duas sub-pastas:
* `Usuários`
* `Computadores`

Em seguida, na sub-pasta `Usuários`, criou-se o primeiro objeto do tipo Usuário:
* **First Name:** Mario | **Last Name:** Silva
* **User logon name:** `mario.silva` (`mario.silva@lab.local`)

![Criação do Usuário Mario Silva](caminho_da_imagem_aqui)

---

### Etapa 16: Definição de Credenciais e Regras do Usuário
* Definição de senha inicial forte.
* **Desmarcado:** *User must change password at next logon*.
* **Marcado:** *Password never expires* (Apenas para otimização das rotinas do laboratório).

![Definição de Senha do Usuário](caminho_da_imagem_aqui)

---

## 5. Instalação e Configuração do Servidor DHCP

### Etapa 17: Instalação da Função Servidor DHCP
No **Server Manager** > `Manage` > `Add Roles and Features`:
* Marcada a caixa **DHCP Server**.
* Confirmada a adição dos recursos adicionais de gerenciamento (*Add Features*).

![Instalação da Função DHCP Server](caminho_da_imagem_aqui)

---

### Etapa 18: Finalização da Instalação do DHCP
Acompanhamento da barra de progresso e conclusão da instalação das ferramentas do DHCP.

![Conclusão da Instalação do DHCP](caminho_da_imagem_aqui)

---

### Etapa 19: Autorização do DHCP no Active Directory (Notificação)
No topo do Server Manager, clicou-se no ícone da bandeira amarela de alerta e em **Complete DHCP configuration** para vincular o serviço ao AD.

![Notificação para Autorizar o DHCP](caminho_da_imagem_aqui)

---

### Etapa 20: Assistente de Autorização do DHCP
* **Credenciais Utilizadas:** `LAB\Administrator`.
* Finalização da autorização garantindo o status **Done** nas etapas de criação de grupos de segurança e autorização no controlador de domínio.

![Autorização do DHCP Concluída com Sucesso](caminho_da_imagem_aqui)

---

### Etapa 21: Criação do Escopo de Distribuição de IPs (*DHCP Scope*)
No console de gerenciamento do DHCP (`Tools` > `DHCP`):
1. Expandido o servidor `dc01.lab.local` > Clique com botão direito em `IPv4` > **New Scope...**
2. **Nome do Escopo:** `LAB_SCOPE`.

![Criação de Novo Escopo IPv4](caminho_da_imagem_aqui)

---

### Etapa 22: Definindo a Faixa de Endereços IP
Configuração do intervalo dinâmico de IPs que serão atribuídos às máquinas clientes:

* **Start IP Address:** `192.168.10.100`
* **End IP Address:** `192.168.10.200`
* **Length:** `24`
* **Subnet Mask:** `255.255.255.0`

![Configuração da Faixa de IP do Escopo](caminho_da_imagem_aqui)

---

### Etapa 23: Exclusões, Duração de Concessão e Opções de DNS
* **Exclusões de IP:** Nenhuma exclusão necessária dentro do bloco 100-200.
* **Lease Duration:** Mantido o padrão de 8 dias.
* **Parent Domain:** `lab.local`
* **DNS Server IP:** `192.168.10.1`

> *Nota:* Ao adicionar o IP `192.168.10.1`, o assistente exibe o alerta *"The IP Address is not a valid DNS address..."*. Isso ocorre porque o servidor está em rede isolada sem internet e a consulta de teste falha. Selecionou-se **Yes** para confirmar a inclusão.

![Inclusão do Servidor DNS no Escopo DHCP](caminho_da_imagem_aqui)

---

### Etapa 24: Limpeza de Entradas e Ativação do Escopo
* Removido qualquer IP residual (ex.: `192.168.0.1`), deixando exclusivamente o IP `192.168.10.1`.
* **WINS Servers:** Mantido em branco.
* Finalizada a configuração marcando a opção de **Ativar o escopo imediatamente**.

![Remoção de IPs Indesejados e Ativação do Escopo](caminho_da_imagem_aqui)

---

## 6. Criação e Configuração da Máquina Cliente (PC01 - Windows 11)

### Etapa 25: Criação da VM do Cliente Windows 11
Criação da máquina virtual no VirtualBox para o sistema operacional cliente:

* **Nome da VM:** `PC01`
* **Desmarcada a opção:** *Proceed with Unattended Installation* (Instalação Não Atendida).
  > *Motivo:* A instalação automatizada do VirtualBox no Windows 11 pode criar usuários genéricos (`vboxuser`) ou causar travamentos em loop na tela OOBE. A instalação manual garante o controle total da criação da conta local temporária.

![Criação da VM PC01 Desmarcando Unattended Installation](caminho_da_imagem_aqui)

---

### Etapa 26: Ajuste da Placa de Rede da VM Cliente
Antes de ligar o `PC01`, configurou-se a placa de rede para o mesmo segmento virtual do servidor:

* **Ligado a:** `Rede Interna`
* **Nome:** `LAB_REDE`

![Ajuste de Rede da VM PC01](caminho_da_imagem_aqui)

---

## 7. Ingresso da Máquina Cliente no Domínio

### Etapa 27: Verificação Inicial de IP no Cliente
No `PC01`, abriu-se o Prompt de Comando (`cmd`) para checar as tabelas de rede via comando:
```cmd
ipconfig /all
