# Projeto 1 - Laboratório de Redes e Suporte

---

## Parte 1 - Configurações Iniciais (1)

Após terminar a instalação do VirtualBox, o download das ISOs do Windows Server 2022 e do Windows 11 e habilitar a virtualização do processador, foram realizadas as primeiras configurações da VM.

- Foi alterado o nome para **"DC01"**
- Carregadas as ISOs dos sistemas operacionais
- Alocada a quantidade correta de memória RAM (4096 MB), número de processadores (2) e quantidade de espaço em disco a ser usado (40 GB)

<img width="945" height="723" alt="1Parte 1 - Configurações Iniciais 1" src="https://github.com/user-attachments/assets/a3d420ca-bde7-4d3a-866b-685164db176e" />


---

## Parte 1 - Configurações Iniciais (2)

Esta tela mostra a maioria das configurações citadas anteriormente, com a VM configurada e pronta para iniciar.

<img width="1919" height="1029" alt="2Parte 1 - Configurações iniciais 2" src="https://github.com/user-attachments/assets/16d6f8c6-633c-477b-961c-874f074685ef" />

---

## Parte 2 - Configurando a Rede

Aqui foram feitas as configurações de rede da VM:

- **"Ligado a":** foi alterado para **"Rede Interna"** para isolar completamente o ambiente de testes da rede física local e da internet, evitando que o servidor DHCP do laboratório gere conflitos com a rede do computador hospedeiro.
- **"Nome":** foi alterado para **"LAB_REDE"**.

<img width="1919" height="1027" alt="3Parte 2 - Configurando a rede" src="https://github.com/user-attachments/assets/68d9cf64-4517-48fe-9748-3d2f1b0ea217" />


---

## Parte 4 - Instalando o Windows Server 2022

A escolha da versão do Windows Server:

Neste caso, a escolha foi **"Windows Server 2022 Datacenter Evaluation (Desktop Experience)"**. Essa opção foi escolhida para garantir a instalação da interface gráfica, já que as opções sem essa marcação instalam o modo *Server Core*, que roda apenas via terminal de linha de comando.

Após finalizar a instalação do sistema, foi definida a senha para o sistema.

<img width="624" height="471" alt="4Parte 3 - Instalando o Windows Server 2022" src="https://github.com/user-attachments/assets/db902897-b8f6-49ee-a20e-6cab95a8802f" />


---

## Parte 5 - Server Manager (1)

Aqui foi dado início à configuração do Server Manager, começando pela definição de um IP estático e confirmação do nome da máquina:

- **Nome do computador:** `"DC01"`
- **Descrição:** `"Lab Server"`

<img width="1920" height="1009" alt="5Parte 4 - Server Manager" src="https://github.com/user-attachments/assets/519e5878-3e7e-4168-8810-830976433a8c" />


---

## Parte 5 - Server Manager (2)

A definição do IP estático foi a seguinte:

- **IP address:** `192.168.10.1`
- **Subnet mask:** `255.255.255.0`
- **Default gateway:** *(Deixado em branco)*
- **Preferred DNS server:** `127.0.0.1` (apontando para ele mesmo)

<img width="1920" height="1009" alt="6Parte  4 - Server Manager 2" src="https://github.com/user-attachments/assets/326b7c20-a709-403d-9bbe-0d25bf128f70" />


---

## Parte 5 - Active Directory (1)

Para a instalação do Active Directory, foram adicionadas funções e recursos (*Add roles and features*).

Em **Server Roles**, foi marcada a caixa **"Active Directory Domain Services"**.

Após isso, foi aberta uma janela pop-up perguntando sobre os recursos adicionais, onde a opção **"Add Features"** foi selecionada.

<img width="1920" height="1009" alt="7Parte 5 - Active Directory" src="https://github.com/user-attachments/assets/6857725a-0739-4e7d-a526-0a149a47594e" />

---

## Parte 5 - Active Directory (2)

Tela de conclusão da instalação do Active Directory.

<img width="1920" height="1009" alt="8Parte 5 - Active Directory 2" src="https://github.com/user-attachments/assets/8423311e-0b75-4597-9bf2-a1c8c36293a3" />


---

## Parte 6 - Promoção do Servidor (1)

Após a instalação do Active Directory, foi iniciada a promoção do servidor.

Em **Deployment Configuration**, foi selecionada a opção **"Add a new forest"**.

No campo **Root domain name**, foi digitado: `lab.local` e clicado em **"Next"**.

<img width="1920" height="1009" alt="9Parte 6 - Promoção do Servidor 1" src="https://github.com/user-attachments/assets/e997aba0-aad8-480c-8761-b63a46a151bb" />

---

## Parte 6 - Promoção do Servidor (2)

Em **"Domain Controller Options"**, foram mantidos os níveis funcionais em Windows Server 2016 (padrão).

Foi definida uma senha para o DSRM (*Directory Services Restore Mode*) e clicado em **"Next"**.

<img width="1920" height="1009" alt="10Parte 6 - Promoção do Servidor 2" src="https://github.com/user-attachments/assets/f776280a-9595-4160-9a8f-3b19ecba9212" />

# Documentação de Configuração - Active Directory & DHCP

---

## Parte 6 - Promoção do Servidor (Etapa 3)

Em **"DNS Options"**, houve um aviso amarelo informando *"A delegation for this DNS server cannot be created..."*. Neste caso, a mensagem foi ignorada por ser um aviso normal, pois é o primeiro servidor DNS da rede.

Foi selecionado **Next**.

<img width="1920" height="1009" alt="11Parte 6 - Promoção do Servidor 3" src="https://github.com/user-attachments/assets/904afb3d-35be-42e2-81bc-dfb720b69621" />


---

## Parte 6 - Promoção do Servidor (Etapa 4)

Em **"Additional Options"**, foi mantido o nome NetBIOS pré-preenchido, neste caso **"LAB"**, e selecionado **Next**.

Foi selecionado **Next** na tela de **"Paths"** e em **"Review Options"**.

<img width="1920" height="1009" alt="12Parte 6 - Promoção do Servidor 4" src="https://github.com/user-attachments/assets/3daba438-b960-4dad-b442-389f834e1235" />

---

## Parte 6 - Promoção do Servidor (Etapa 5)

Em **"Prerequisites Check"**, o assistente fez uma verificação de pré-requisitos.

Após surgir a mensagem com ícone verde no topo (*"All prerequisite checks passed successfully"*), foi selecionado **Install**.

<img width="1920" height="1009" alt="13Parte 6 - Promoção do Servidor 5" src="https://github.com/user-attachments/assets/cb6e0f95-2d90-40ad-840e-9eadc2e2f4aa" />

---

## Parte 7 - Unidade Organizacional (Etapa 1)

Para criar a unidade organizacional, foi aberta a ferramenta de gerenciamento do AD.

No **Server Manager**, foi selecionado no menu superior **Tools** > **Active Directory Users and Computers**.

Na janela aberta, foi expandida a seta ao lado do domínio **"lab.local"** no painel esquerdo.

Foi clicado com o botão direito em cima de **"lab.local"**, selecionado **New** e depois **Organizational Unit**.

Foi digitado o nome **"LAB_Empresa"** e verificado se a opção **"Protect container from accidental deletion"** estava marcada.

Foi selecionado **OK**, e assim foi criada a primeira pasta da Unidade Organizacional.

<img width="1920" height="1009" alt="14Parte 7 - Unidade Organizacional 1" src="https://github.com/user-attachments/assets/c05ecb43-4cb1-4ac7-be28-b676cbb0729d" />


---

## Parte 7 - Unidade Organizacional (Etapa 2)

Agora foram criadas duas subpastas dentro dela:

1. Foi clicado com o botão direito em **LAB_Empresa**.
2. Foram selecionados **New** e **Organizational Unit**, e digitado **"Usuários"**.
3. Foi repetido o mesmo processo para a criação de outra subpasta nomeada **"Computadores"**.

Para criar o primeiro Usuário do Domínio, foi clicado com o botão direito dentro da subpasta **"Usuários"**.

Foi selecionado **New** e depois **User**.

Foram preenchidos os campos de identificação:
- **First name:** Mario
- **Last name:** Silva *(nome fictício)*
- **User logon name:** `mario.silva` *(definido como login de acesso)*

Foi selecionado **Next**.

<img width="1920" height="1009" alt="15Parte 7 - Unidade Organizacional 2" src="https://github.com/user-attachments/assets/3e11f7b2-b6c1-41f1-8dd2-c17cf990c315" />


---

## Parte 7 - Unidade Organizacional (Etapa 3)

Na tela de senha, foi digitada uma senha forte.

- Foi desmarcada a opção **"User must change password at next logon"**.
- Foi marcada a opção **"Password never expires"** para facilitar o laboratório.

Foi selecionado **Next** e depois **Finish**.

Com isso, o usuário `mario.silva@lab.local` já existe no banco de dados e poderá ser usado para fazer login na máquina cliente (Windows 11) assim que for integrada à rede.

<img width="1920" height="1009" alt="16Parte 7 - Unidade Organizacional 3" src="https://github.com/user-attachments/assets/3ac26d83-0c26-43bb-92e9-8ca79d8b5792" />


---

## Parte 8 - Instalando a Função de Servidor DHCP (Etapa 1)

No **Server Manager**, foi selecionado **Manage** e, após isso, **Add Roles and Features**.

Foi selecionado **Next** nas telas iniciais até chegar em **Server Roles**.

A caixa **DHCP Server** foi marcada.

Na janela pop-up que apareceu, foi selecionado **Add Features** e depois **Next**.

<img width="1920" height="1009" alt="17Parte 8 - Instalando a Função de Servidor DHCP 1" src="https://github.com/user-attachments/assets/a83e50a7-e90c-412e-b8e1-b459181c730b" />


---

## Parte 8 - Instalando a Função de Servidor DHCP (Etapa 2)

Foi selecionado **Next** nas telas de **"Features"** e **"DHCP Server"**, até chegar à tela de **"Confirmation"**, onde foi selecionado **Install**.

Após a conclusão da instalação, foi selecionado **Close**.

<img width="1920" height="1009" alt="18Parte 8 - Instalando a Função de Servidor DHCP 2" src="https://github.com/user-attachments/assets/9450fc3d-3e44-417f-9c3e-abf36e278074" />


---

## Parte 9 - Autorizando o DHCP no Active Directory (Etapa 1)

No topo do **Server Manager**, foi clicado no ícone da **bandeira com alerta amarelo** e selecionado **Complete DHCP configuration**.

<img width="1920" height="1009" alt="19Parte 9 - Autorizando o DHCP no Active Directory 1" src="https://github.com/user-attachments/assets/4aaee6a4-75b9-4afd-8112-c29e71ef3036" />


---

## Parte 9 - Autorizando o DHCP no Active Directory (Etapa 2)

Na janela que se abriu, foi selecionado **Next**.

Em **Authorization**, certificou-se de que a opção **"Use the following user's credentials"** estava selecionada com o usuário `LAB\Administrator`.

Foi selecionado **Commit**.

Verificou-se que o status de ambas as etapas aparecia como **"Done"**.

E foi selecionado **Close**.

<img width="1920" height="1009" alt="20Parte 9 - Autorizando o DHCP no Active Directory 2" src="https://github.com/user-attachments/assets/cf6a12ae-4c74-4814-9119-ea4375eb5d52" />


---

## Parte 10 - Criando o Escopo de IPs (DHCP Scope)

No menu superior do Server Manager, foi selecionado **"Tools"** e **"DHCP"**.

No painel esquerdo, foi expandido o nome do servidor **"(dc01.lab.local)"**.

Foi clicado com o botão direito sobre a opção **"IPv4"**.

E selecionado **"New Scope..."**.

Foi selecionado **"Next"** no assistente.

Em **"Name"** foi digitado `"LAB_SCOPE"`.

E selecionado **"Next"**.

<img width="1920" height="1009" alt="21Parte 10 - Criando o Escopo de IPs (DHCP Scope)" src="https://github.com/user-attachments/assets/5045d0cc-d03a-4d3d-a471-ea62c142f7c3" />


---

## Parte 10 - Criando o Escopo de IPs (DHCP Scope) - Parte 2

**"IP Address Range"** foi preenchido com a faixa da rede:

- **Start IP address:** `192.168.10.100`
- **End IP address:** `192.168.10.200`
- **Length:** `24`
- **Subnet mask:** `255.255.255.0`

Foi selecionado **"Next"**.

<img width="1920" height="1009" alt="22Parte 10 - Criando o Escopo de IPs (DHCP Scope) 2" src="https://github.com/user-attachments/assets/e6a62f40-2ef2-4535-809b-bb5b43007ec6" />


---

## Parte 10 - Criando o Escopo de IPs (DHCP Scope) - Parte 3

Em **"Add Exclusions and Delay"** não foi preciso excluir nada dentro da faixa `100-200`.

Foi selecionado **"Next"**.

Para **"Lease Duration"** foi mantido o padrão de `8 dias`.

E selecionado **"Next"**.

Em **"Configure DHCP Options"** clicado em **"Next"**.

Em **"Router (Default Gateway)"**, como a rede do projeto é isolada e não tem roteador, foi apenas selecionado **"Next"** sem preencher.

Os campos de **"Domain Name and DNS Servers"** foram preenchidos da seguinte forma:

- **Parent domain:** `lab.local`
- **IP address:** `192.168.10.1`

E foi selecionado **"Add"**, o nome será resolvido para `"dc01.lab.local"`.

Após **"Add"** ser selecionado, apareceu o seguinte aviso: *"The IP Address 192.168.10.1 is not a valid DNS address, do you still want to add it?"*. Esse aviso aparece porque o assistente do DHCP tenta enviar uma consulta de teste para o IP `192.168.10.1` para confirmar se ele responde como DNS. Como o servidor está em uma rede interna isolada sem internet, a validação automática falha e exibe esse alerta.

Na caixa de diálogo aberta foi selecionado **"Yes"**.

<img width="1920" height="1009" alt="23Parte 10 - Criando o Escopo de IPs (DHCP Scope) 3" src="https://github.com/user-attachments/assets/0ac9ecdb-617e-4dd1-a7c1-9c48f2815126" />


---

## Parte 10 - Criando o Escopo de IPs (DHCP Scope) - Parte 4

Foi clicado em cima do IP `"192.168.0.1"`.

E no botão **"Remove"** ao lado.

Apenas o IP `"192.168.10.1"` permaneceu na lista.

Foi selecionado **"Next"** para continuar a configuração do escopo.

**"WINS Servers"** foi deixado em branco.

E selecionado **"Next"**.

Em **"Activate Scope"**, foi clicado em **"Finish"**.

<img width="1920" height="1009" alt="24Parte 10 - Criando o Escopo de IPs (DHCP Scope) 4" src="https://github.com/user-attachments/assets/97217f23-a260-4197-a699-347ec4ca11e9" />


---

## Parte 11 - Criação da Máquina Cliente (Windows 11)

Aqui as configurações foram praticamente as mesmas da criação do Servidor (Windows Server 2022), as únicas diferenças foram:

- **VM Name:** `PC01`
- E a desmarcação da opção **"Proceed with Unattended Installation"**. Embora a instalação automatizada funcione bem no Windows Server, no Windows 11 do VirtualBox ela costuma gerar pequenos problemas:
  - **Criação de usuário genérico:** O VirtualBox tenta criar automaticamente uma conta chamada `"vboxuser"` com senha padrão, o que pode causar confusão depois na hora de fazer o login local.
  - **Bugs na finalização:** É comum o script automatizado do VirtualBox travar ou entrar em loop na tela de preparação inicial (OOBE) do Windows 11.

Ao realizar a instalação manual tradicional:

- Você evita falhas de scripts do VirtualBox.
- Você cria seu próprio usuário local temporário (ex: `adminlocal`).
- O processo de instalação segue o padrão exato de um computador físico corporativo.

<img width="784" height="527" alt="25Parte 11 - Criação da Máquina Cliente" src="https://github.com/user-attachments/assets/17facd46-7663-4360-b1aa-73c93e6841a7" />


---

## Parte 12 - Configurando a Rede da Máquina Cliente

Antes de ligar a VM, é necessário colocá-la no mesmo segmento de rede virtual do **"DC01"** (Servidor):

1. A VM **"PC01"** foi selecionada.
2. Em seguida, foi clicado em **"Configurações"** e **"Rede"**.
3. Na aba **Placa 1**, foram definidos os seguintes parâmetros:
   - **Ligado a:** Rede Interna
   - **Nome:** `LAB_REDE` (pois deve ser o mesmo nome usado no servidor)
4. Foi selecionado **"OK"**.

<img width="901" height="486" alt="26Parte 12 - Configurando a Rede da Máquina Cliente" src="https://github.com/user-attachments/assets/1c84f94d-49a2-41b3-bbdf-6287534cdeab" />


---

## Parte 13 - Validando o IP no Cliente

No PC01, foi aberto o menu **"Iniciar"**, digitado `cmd` e aberto o **"Prompt de Comando"**.

Foi digitado o seguinte comando: `ipconfig /all`

E apertado **"Enter"**.

<img width="1920" height="1009" alt="27Parte 13 - Validando o IP no Cliente" src="https://github.com/user-attachments/assets/83b82741-6292-4b24-bfc6-6f9498724c1b" />


---

## Parte 14 - Voltando o PC01 para IP Automático (DHCP) - Parte 1

No PC01, foi pressionado `Win + R`.

Digitado `ncpa.cpl` e apertado **"Enter"**.

Foi clicado com o botão direito em **"Ethernet"**, **"Propriedades"** e dado duplo clique em **"Protocolo IP Versão 4 (TCP/IPv4)"**.

Foram marcadas as duas opções para automático:

- **"Obter um endereço IP automaticamente"**
- **"Obter o endereço dos servidores DNS automaticamente"**

E clicado em **"OK"** e **"OK"**.

<img width="1920" height="1009" alt="28Parte 14 - Voltando o PC01 para IP Automático (DHCP) 1" src="https://github.com/user-attachments/assets/6d8d969a-def8-4e86-b62c-83aec08bff60" />


---

## Parte 14 - Voltando o PC01 para IP Automático (DHCP) - Parte 2

No Prompt de Comando (CMD) do PC01, foi executado o comando: `ipconfig /renew`

Em seguida, foi executado o comando: `ipconfig /all`

Confirmando o recebimento do IP `"192.168.10.100"` e o DNS Server `"192.168.10.1"`.

<img width="1920" height="1009" alt="29Parte 14 - Voltando o PC01 para IP Automático (DHCP) 2" src="https://github.com/user-attachments/assets/6e8cc402-1ebc-4e95-aadc-0ca4ea0aca38" />


---

## Parte 15 - Testando a Resolução do Domínio (DNS) - Parte 1

No CMD do PC01, foi executado: `nslookup lab.local`

O comando retornou o nome do servidor e o endereço `"192.168.10.1"`.

<img width="1920" height="1009" alt="30Parte 15 - Testando a Resolução do Domínio (DNS) 1" src="https://github.com/user-attachments/assets/b519f662-359e-4df8-a2ad-84bd03260dcd" />


---

## Parte 15 - Testando a Resolução do Domínio (DNS) 2

No PC01, foi pressionado `Win + R`.

Digitado `sysdm.cpl`.

E pressionado `Enter`, o que abrirá as "Propriedades do Sistema".

Na aba "Nome do Computador", foi selecionado o botão "Alterar..." (Change...).

Na seção "Membro de", foi selecionada a opção "Domínio" (Domain).

E digitado `lab.local`.

E clicado em "OK".

<img width="1920" height="1009" alt="31Parte 15 - Testando a Resolução do Domínio (DNS) 2" src="https://github.com/user-attachments/assets/0f9852c9-03e0-43b2-9a70-b0915dfac2d5" />



---

## Parte 15 - Testando a Resolução do Domínio (DNS) 3

A mensagem "Sign in to: LAB" logo abaixo do campo de senha confirma que a máquina já está autenticando diretamente ao servidor "Active Directory".

<img width="1920" height="1009" alt="32Parte 15 - Testando a Resolução do Domínio (DNS) 3" src="https://github.com/user-attachments/assets/795cdc31-f3d0-46c3-a7a7-5a526e590ee6" />



---

## Parte 16 - Criando grupos

Na VM do DC01, foi pressionado `Win + R`.

Digitado `dsa.msc`.

E pressionado `Enter`.

Na árvore do lado esquerdo, foi expandido o domínio `lab.local`.

Foi clicado com o botão direito em "Usuários".

Em seguida em "Novo" (New) e "Grupo" (Group).

Agora, para criar o Grupo "TI":

Na janela "Novo Objeto - Grupo" (New Object - Group), foram preenchidos os seguintes dados:
- **Group name:** TI
- **Group scope:** Global
- **Group type:** Security

E clicado em "OK".

Foi repetido o mesmo processo para os demais grupos: "RH", "Financeiro" e "Suporte", mantendo o `Group scope: Global` e `Group type: Security`.

<img width="1920" height="1009" alt="33Parte 16 - Criando grupos" src="https://github.com/user-attachments/assets/ff7980b1-c424-4258-a184-bf1e1050aac1" />



---

## Parte 17 - Adicionando o Usuário ao Grupo

Para vincular o usuário `mario.silva` ao grupo "TI", foi clicado com o botão direito no grupo "TI".

E selecionado "Propriedades (Properties)".

Na aba "Membros (Members)", foi clicado em "Adicionar... (Add...)".

Foi digitado `mario.silva`.

Clicado em "Verificar Nomes (Check Names)".

Depois em "OK".

E finalmente "Aplicar" e "OK".

<img width="1920" height="1009" alt="34Parte 17 - Adicionando o Usuário ao Grupo" src="https://github.com/user-attachments/assets/d177ecfa-5868-4930-93c2-b4c6581510cd" />



---

## Parte 18 - Implementando o File Server

Para criar a estrutura de pastas no DC01, foi aberto o "Explorador de Arquivos (File Explorer)".

E navegado até `C:\`.

Foi criada uma pasta chamada "Compartilhamento".

Foi entrado na pasta `C:\Compartilhamento` e criadas três subpastas:
- TI
- RH
- Financeiro

<img width="1920" height="1009" alt="35Parte 18 - Implementando o File Server" src="https://github.com/user-attachments/assets/d0ae0b72-8710-4361-aed6-8fee632744c8" />



---

## Parte 19 - Compartilhando a Pasta Principal na Rede

Foi clicado com o botão direito na pasta `C:\Compartilhamento`.

E selecionado "Properties (Propriedades)".

Na aba "Sharing (Compartilhamento)", foi clicado em "Advanced Sharing... (Compartilhamento Avançado...)".

Foi marcada a caixa "Share this folder (Compartilhar esta pasta)".

Foi clicado no botão "Permissions (Permissões)".

Foi garantido que o grupo "Everyone (Todos)" tenha permissão de "Full Control (Controle Total)" ou "Change (Alteração)".

> **Nota de arquitetura:** No Windows Server, liberamos o acesso de rede na pasta raiz e controlamos quem pode fazer o que através da aba "Security (NTFS)" nas subpastas.

Foi clicado em "OK", "OK" e fechada a janela.

<img width="1920" height="1009" alt="36Parte 19 - Compartilhando a Pasta Principal na Rede" src="https://github.com/user-attachments/assets/2cfd23b6-db9a-431a-a7f6-2f58fa75a528" />



---

## Parte 20 - Configurando Permissões da Pasta TI (Quebra de Herança)

Foi clicado com o botão direito na pasta `C:\Compartilhamento\TI`.

E selecionado "Properties (Propriedades)".

Na aba "Security (Segurança)", foi clicado no botão "Advanced (Avançado)".

Na parte inferior, foi clicado em "Disable inheritance (Desabilitar herança)".

Foi selecionada a opção "Convert inherited permissions into explicit permissions... (Converter permissões herdadas em permissões explícitas...)".

Foi selecionado o grupo genérico "Users (Usuários)" da lista.

E clicado em "Remove (Remover)".

Foi clicado em "OK" para voltar à tela anterior.

<img width="1920" height="1009" alt="37Parte 20 - Configurando Permissões da Pasta TI (Quebra de Herança)" src="https://github.com/user-attachments/assets/3cd2945c-014a-4cda-bce2-b986a8cfe3c8" />



---

## Parte 21 - Adicionando os Grupos e Definindo Permissões 1

Ainda na aba "Security" da pasta TI:

Foi clicado em "Edit... (Editar...)" para definir os acessos para o Grupo TI (Acesso de Modificação).

Foi clicado em "Add... (Adicionar...)".

Digitado `TI`.

Clicado em "Check Names" e dado "OK".

<img width="1920" height="1009" alt="38Parte 21 - Adicionando os Grupos e Definindo Permissões" src="https://github.com/user-attachments/assets/c114981e-dbe8-4dc7-bb77-35b0101cdcfc" />



---

## Parte 22 - Adicionando os Grupos e Definindo Permissões 2

Foi marcada a caixa "Modify (Modificar)" na coluna "Allow (Permitir)".

Clicado em "Apply" e dado "OK".

<img width="1920" height="1009" alt="39Parte 22 - Adicionando os Grupos e Definindo Permissões 2" src="https://github.com/user-attachments/assets/88a4329d-16d3-4ad1-b92e-ab0ec57d2f45" />



---

## Parte 23 - Adicionando os Grupos e Definindo Permissões 3

Para o Grupo "RH" (Acesso de Leitura):

Foi clicado em "Add... (Adicionar...)".

Digitado `RH`.

Clicado em "Check Names" e dado "OK".

<img width="1920" height="1009" alt="40Parte 23 - Adicionando os Grupos e Definindo Permissões 3" src="https://github.com/user-attachments/assets/15bdb778-1c9f-4a36-ad3a-c5f071f12f46" />


---

## Parte 23 - Adicionando os Grupos e Definindo Permissões 4

Foram mantidas apenas as caixas de "Read & execute" e "Read (Leitura)" marcadas.

**Grupo Financeiro (Sem Acesso):**

No modelo de segurança do Windows, não foi adicionado o grupo "Financeiro" à lista pois a ausência do grupo na lista garante automaticamente o "acesso negado (No access)".

Foi clicado em "Apply" e "OK".

<img width="1920" height="1009" alt="41Parte 23 - Adicionando os Grupos e Definindo Permissões 4" src="https://github.com/user-attachments/assets/2667375a-c827-4583-9110-2ca4856c5222" />



---

## Parte 24 - Testando o Acesso no PC01 1

No PC01 (logado com o usuário `mario.silva`):

Foi pressionado `Win + R`.

Digitado o caminho da rede do servidor: `\\DC01\Compartilhamento`.

E apertado `Enter`.

<img width="1920" height="1009" alt="42Parte 24 - Testando o Acesso no PC01 1" src="https://github.com/user-attachments/assets/246b2b00-44df-4b70-95da-dab5a52d1b63" />


---

## Parte 24 - Testando o Acesso no PC01 2

Como o Mário pertence ao grupo "TI", foi feita a tentativa de criar um arquivo de texto dentro dela, porém o aviso "Network Error" foi mostrado. Esse erro acontece por um detalhe muito comum no Active Directory: o Windows só carrega os novos grupos de um usuário no momento em que ele faz o login. Como o Mário já estava logado no PC01 quando foi adicionado ao grupo "TI" no servidor, a máquina cliente ainda não recebeu essa permissão.

<img width="1920" height="1009" alt="43Parte 24 - Testando o Acesso no PC01 2" src="https://github.com/user-attachments/assets/09205f89-cf1b-4774-9b76-6cd1f0f9f5c7" />


---

## Parte 24 - Testando o Acesso no PC01 3

Para resolver esse problema, foi feito logoff e login novamente no PC01.

Para validar o "Token de Segurança" no PC01 após fazer login novamente, foi aberto o "Prompt de Comando (CMD)" no PC01.

E executado `whoami /groups`.

Foi conferido se o grupo `LAB\TI` apareceu listado no resultado, porém não apareceu, o que significa que o Kerberos (sistema de autenticação do Windows) ainda não emitiu um novo bilhete de segurança com a lista de grupos atualizada para o Mário.

<img width="1920" height="1009" alt="44Parte 24 - Testando o Acesso no PC01 3" src="https://github.com/user-attachments/assets/34510e17-1573-4c1f-b376-50ad749e024b" />



---

## Parte 24 - Testando o Acesso no PC01 4

Para resolver esse problema, foram seguidos os passos abaixo:

### Passo 1 - Verificando a Associação no DC01:

No servidor, voltou-se à VM do DC01.

Foi aberto o "Active Directory (`dsa.msc`)".

Em seguida, foi selecionado "LAB_Empresa" e "Usuários".

E dado um duplo clique no usuário "Mario Silva".

Foi clicado na aba "Member Of (Membro de)".

E confirmado se o grupo "TI" está realmente aparecendo nessa lista.

Como não estava, foi clicado em "Add...".

Digitado `TI`.

Clicado em "Check Names".

E dado "OK".

Depois foi clicado em "Apply" e "OK".

<img width="1920" height="1009" alt="45Parte 24 - Testando o Acesso no PC01 4" src="https://github.com/user-attachments/assets/070362dd-49f8-4009-a4f7-d62aff329a03" />



---

## Parte 24 - Testando o Acesso no PC01 5

### Passo 2 - Fazendo Logoff Completo no PC01:

Na máquina cliente, o Windows só reconstrói a lista de grupos durante um "logoff real" (bloquear a tela ou reiniciar sem encerrar a sessão não atualiza os tokens em cache imediatamente).

No PC01, foi clicado no menu "Iniciar".

Clicado no ícone do usuário `mario.silva`.

E escolhido "Sign out (Sair)".

Na tela de login, entrou-se novamente com a conta `mario.silva` e a senha.

### Passo 3 - Validar novamente no CMD:

Na máquina cliente, foi aberto o Prompt de Comando (CMD) normal.

Digitado o comando `whoami /groups` novamente.

O grupo `LAB\TI` agora apareceu listado no meio do resultado.

<img width="1920" height="1009" alt="46Parte 24 - Testando o Acesso no PC01 5" src="https://github.com/user-attachments/assets/362e20b7-f614-4e51-96a6-67cd28ffef9e" />


---

## Parte 24 - Testando o Acesso no PC01 6

Foi aberto novamente o caminho `\\DC01\Compartilhamento\TI` pelo "Executar (`Win + R`)".

E criado um "Text Document (Documento de Texto)", dessa vez sem avisos.

<img width="1920" height="1009" alt="47Parte 24 - Testando o Acesso no PC01 6" src="https://github.com/user-attachments/assets/463a7ccf-593e-4844-8c27-4d0ba7192548" />



---

## Parte 25 - Criando uma política simples com Group Policy 1

No DC01, foram pressionadas as teclas `Win + R`.

Digitado `gpmc.msc`.

E pressionado `Enter`.

<img width="1920" height="1009" alt="48Parte 25 - Criando uma política simples com Group Policy 1" src="https://github.com/user-attachments/assets/d758034a-f13d-4e15-82c0-89722d167ae1" />



---

## Parte 26 - Criando uma política simples com Group Policy 2

Para abrir o "Gerenciador de Diretivas de Grupo", na árvore da esquerda, foram expandidos os seguintes itens: `Forest > lab.local > Domains > lab.local`.

Foi clicado com o botão direito em "Default Domain Policy".

E selecionado "Edit... (Editar...)".

Para localizar as configurações de senha no "Group Policy Management Editor", na janela do editor que se abriu, foi navegado pela árvore no lado esquerdo até o seguinte caminho:

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy`

Para configurar o tamanho mínimo e complexidade da senha, na pasta "Password Policy", foi clicado duas vezes sobre "Minimum password length".

Foi marcada a caixa "Define this policy setting".

Alterado o valor para 8 (caracteres).

E clicado em "OK".

<img width="1920" height="1009" alt="49Parte 25 - Criando uma política simples com Group Policy 2" src="https://github.com/user-attachments/assets/a40455ab-942a-42af-8db0-fa7de9908a17" />


---

## Parte 26 - Criando uma política simples com Group Policy 3

Em relação à "Complexidade de Senha", foi clicado duas vezes sobre "Password must meet complexity requirements".

Foi marcada a caixa "Define this policy setting".

Selecionado "Enabled (Habilitado)" para exigir letras maiúsculas, minúsculas e números/símbolos.

E clicado em "OK".

<img width="1920" height="1009" alt="50Parte 26 - Criando uma política simples com Group Policy 3" src="https://github.com/user-attachments/assets/040ee490-02ee-4a1c-8d1a-9ff68319326f" />


---

## Parte 27 - Testando a Política de Senhas 1

Foi pressionado "Win + R".

Depois digitado "dsa.msc".

Pressionado "Enter".

E foi navegado até a OU onde está o usuário de teste, "lab.local > LAB_Empresa > Usuários".

Agora foi realizado o teste para redefinir a senha para uma senha fraca, foi clicado com o botão direito sobre o usuário "Mario Silva".

E escolhido "Reset Password... (Redefinir senha...)".

Foi digitada uma senha que não atendia aos requisitos e desmarcada a opção "User must change password at next logon", para facilitar o teste.

Foi clicado em "OK".

<img width="1920" height="1009" alt="51Parte 27 - Testando a Política de Senhas 1" src="https://github.com/user-attachments/assets/bc89bebc-0223-497e-b115-bea5c117cad1" />


---

## Parte 27 - Testando a Política de Senhas 2

Resultado: O Windows Server exibiu uma mensagem de erro informando que a senha não cumpre os requisitos mínimos de tamanho ou complexidade da diretiva do domínio (The password does not meet the password policy requirements).

<img width="1920" height="1009" alt="52Parte 27 - Testando a Política de Senhas 2" src="https://github.com/user-attachments/assets/ae0bee41-fd38-47fc-97cf-3c91de5a7a2c" />


---

## Parte 27 - Testando a Política de Senhas 3

Agora foi feito o teste para redefinir para uma senha forte, foi clicado novamente com o botão direito em "Mario Silva > Reset Password...".

Foi digitada uma senha que atendeu a todos os requisitos.

E clicado em "OK".

Resultado: O Active Directory exibiu a mensagem de confirmação: "The password for Mario Silva has been changed."

<img width="1920" height="1009" alt="53Parte 27 - Testando a Política de Senhas 3" src="https://github.com/user-attachments/assets/bf489b41-f66f-4ba6-b46d-50c90c016726" />


---

## Parte 28 - Criando uma estrutura mais profissional 1

Para criar as "Unidades Organizacionais (OUs) Principais" foi pressionado "Win + R".

Digitado "dsa.msc".

E pressionado "Enter".

Foi clicado com o botão direito no nome do domínio "lab.local".

Foi selecionado "New (Novo) > Organizational Unit (Unidade Organizacional)".

Digitado "TI".

E clicado em "OK".

<img width="1920" height="1009" alt="54Parte 28 - Criando uma estrutura mais profissional 1" src="https://github.com/user-attachments/assets/087a9957-018c-4981-8af1-66b2c17e7ce1" />


---

## Parte 28 - Criando uma estrutura mais profissional 2

Para "Criar as Sub-OUs em Cada Departamento" foi clicado com o botão direito na OU "TI > New > Organizational Unit".

Foi nomeada como "Usuários".

E clicado em "OK".

Foi clicado com o botão direito novamente na OU "TI > New > Organizational Unit".

Foi nomeada como "Computadores".

E clicado em "OK".

Foi repetida essa subcriação "Usuários e Computadores" dentro de "RH, Financeiro e Suporte".

<img width="1920" height="1009" alt="55Parte 28 - Criando uma estrutura mais profissional 2" src="https://github.com/user-attachments/assets/098359ec-29d8-48ff-80ab-01dae31f5fca" />

---

## Parte 28 - Criando uma estrutura mais profissional 3

Para mover os "Objetos Existentes para os Novos Locais" como o "Usuário: Mario Silva", foi clicado nele com o botão direito.

E depois em "Move... (Mover...)".

E selecionado o caminho "lab.local > TI > Usuários".

<img width="1920" height="1009" alt="56Parte 28 - Criando uma estrutura mais profissional 3" src="https://github.com/user-attachments/assets/225b3fb5-651f-4698-8aac-b3f4565a6bb0" />


---

## Parte 28 - Criando uma estrutura mais profissional 4

Para mover o computador foi clicado com o botão direito no computador "PC01".

Depois em "Move...".

E selecionado "lab.local > TI > Computadores".

Com isso, o Active Directory ficou profissional e pronto para receber GPOs direcionadas a setores específicos.

![Print - Parte 28 - Criando uma estrutura mais profissional 4](caminho_do_print.png)

---

<img width="1920" height="1009" alt="57Parte 28 - Criando uma estrutura mais profissional 4" src="https://github.com/user-attachments/assets/237e9b95-c759-409c-b4c2-474e1a478158" />


Para criar mais usuários no Active Directory, no "DC01", foi aberto o "Active Directory Users and Computers (dsa.msc)".

Foi navegado até a OU de destino, "lab.local > RH > Usuários".

Foi clicado com o botão direito na pasta "Usuários > New (Novo) > User (Usuário)".

Foram preenchidos os campos:

First name: Maria  
User logon name: maria  

E clicado em "Next".

<img width="1920" height="1009" alt="58Parte 29 - Criando mais usuários no Active Directory 1" src="https://github.com/user-attachments/assets/236f28c5-6198-4202-9ec8-897fb3e40ebf" />

---

## Parte 29 - Criando mais usuários no Active Directory 2

Para definir a senha e regras, no "DC01", foi digitada uma senha forte, foi desmarcado "User must change password at next logon (O usuário deve alterar a senha no próximo logon)".

Foi marcado "Password never expires (A senha nunca expira)" para facilitar os testes do laboratório.

Foi clicado em "Next".

E depois em "Finish".

<img width="1920" height="1009" alt="59Parte 29 - Criando mais usuários no Active Directory 2" src="https://github.com/user-attachments/assets/cc8eebda-84d3-4f6e-b3da-296ca56b9594" />


---

## Parte 29 - Criando mais usuários no Active Directory 3

Para adicionar o usuário ao grupo de segurança, no "DC01", foi clicado com o botão direito sobre o usuário "Maria", e escolhido "Properties (Propriedades)".

Foi acessada a aba "Member Of (Membro de)".

E clicado em "Add...".

Foi digitado "RH".

Foi clicado em "Check Names".

E dado "OK".

Por fim, foi clicado em "Apply" e "OK".

<img width="1920" height="1009" alt="60Parte 29 - Criando mais usuários no Active Directory 3" src="https://github.com/user-attachments/assets/12073534-5c96-491c-a758-b1d02afd60ca" />


---

## Parte 29 - Criando mais usuários no Active Directory 4

Foi repetido o processo para os outros dois usuários:

João: Foi criado em "Financeiro > Usuários", com "login joao".  
E adicionado ao grupo "Financeiro".  

Maria: Foi criada em "Suporte > Usuários", com "login maria".  
E adicionada ao grupo "Suporte".  

<img width="1920" height="1009" alt="61Parte 29 - Criando mais usuários no Active Directory 4" src="https://github.com/user-attachments/assets/92ef030d-8551-47f2-b96b-c97ffb754eeb" />


---

## Parte 30 - Criando a GPO de Mapeamento de Rede 1

No "DC01", foi aberto o "Group Policy Management (Win + R > gpmc.msc)".

E clicado com o botão direito sobre a raiz do domínio "lab.local > Create a GPO in this domain, and Link it here...".

A GPO foi nomeada como "GPO - Mapeamento Disco Z".

E clicado em "OK".

<img width="1920" height="1009" alt="62Parte 30 - Criando a GPO de Mapeamento de Rede" src="https://github.com/user-attachments/assets/ac04a8de-5c2d-4adc-b321-8d4bba2031a3" />


---

## Parte 30 - Criando a GPO de Mapeamento de Rede 2

Foi clicado com o botão direito na GPO criada e selecionado "Edit... (Editar)".

Para configurar a unidade mapeada, no "Editor de GPO", foi navegado pela árvore no painel esquerdo, "User Configuration > Preferences > Windows Settings > Drive Maps".

Foi clicado com o botão direito no painel direito, "New > Mapped Drive".

Foi preenchida a janela de configuração:

Action: Update  
Location: \\DC01\Compartilhamento  
Drive Letter: Z  
Label as: Arquivos da Empresa  

E finalmente clicado em "Apply" e "OK".

<img width="1920" height="1009" alt="63Parte 30 - Criando a GPO de Mapeamento de Rede 2" src="https://github.com/user-attachments/assets/6b2ae082-8f79-4f8e-b09b-49fc31cd555b" />


---

## Parte 30 - Criando a GPO de Mapeamento de Rede 3

Para testar no cliente, no "PC01" foi aberto o "CMD" e executado "gpupdate /force".

<img width="1920" height="1009" alt="64Parte 30 - Criando a GPO de Mapeamento de Rede 3" src="https://github.com/user-attachments/assets/cc09f124-a3bf-4707-a175-59d6aa5596de" />
