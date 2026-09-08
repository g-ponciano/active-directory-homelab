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

![Print - Promoção do Servidor 3](caminho/para/imagem_parte6_3.png)

---

## Parte 6 - Promoção do Servidor (Etapa 4)

Em **"Additional Options"**, foi mantido o nome NetBIOS pré-preenchido, neste caso **"LAB"**, e selecionado **Next**.

Foi selecionado **Next** na tela de **"Paths"** e em **"Review Options"**.

![Print - Promoção do Servidor 4](caminho/para/imagem_parte6_4.png)

---

## Parte 6 - Promoção do Servidor (Etapa 5)

Em **"Prerequisites Check"**, o assistente fez uma verificação de pré-requisitos.

Após surgir a mensagem com ícone verde no topo (*"All prerequisite checks passed successfully"*), foi selecionado **Install**.

![Print - Promoção do Servidor 5](caminho/para/imagem_parte6_5.png)

---

## Parte 7 - Unidade Organizacional (Etapa 1)

Para criar a unidade organizacional, foi aberta a ferramenta de gerenciamento do AD.

No **Server Manager**, foi selecionado no menu superior **Tools** > **Active Directory Users and Computers**.

Na janela aberta, foi expandida a seta ao lado do domínio **"lab.local"** no painel esquerdo.

Foi clicado com o botão direito em cima de **"lab.local"**, selecionado **New** e depois **Organizational Unit**.

Foi digitado o nome **"LAB_Empresa"** e verificado se a opção **"Protect container from accidental deletion"** estava marcada.

Foi selecionado **OK**, e assim foi criada a primeira pasta da Unidade Organizacional.

![Print - Unidade Organizacional 1](caminho/para/imagem_parte7_1.png)

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

![Print - Unidade Organizacional 2](caminho/para/imagem_parte7_2.png)

---

## Parte 7 - Unidade Organizacional (Etapa 3)

Na tela de senha, foi digitada uma senha forte.

- Foi desmarcada a opção **"User must change password at next logon"**.
- Foi marcada a opção **"Password never expires"** para facilitar o laboratório.

Foi selecionado **Next** e depois **Finish**.

Com isso, o usuário `mario.silva@lab.local` já existe no banco de dados e poderá ser usado para fazer login na máquina cliente (Windows 11) assim que for integrada à rede.

![Print - Unidade Organizacional 3](caminho/para/imagem_parte7_3.png)

---

## Parte 8 - Instalando a Função de Servidor DHCP (Etapa 1)

No **Server Manager**, foi selecionado **Manage** e, após isso, **Add Roles and Features**.

Foi selecionado **Next** nas telas iniciais até chegar em **Server Roles**.

A caixa **DHCP Server** foi marcada.

Na janela pop-up que apareceu, foi selecionado **Add Features** e depois **Next**.

![Print - Função DHCP 1](caminho/para/imagem_parte8_1.png)

---

## Parte 8 - Instalando a Função de Servidor DHCP (Etapa 2)

Foi selecionado **Next** nas telas de **"Features"** e **"DHCP Server"**, até chegar à tela de **"Confirmation"**, onde foi selecionado **Install**.

Após a conclusão da instalação, foi selecionado **Close**.

![Print - Função DHCP 2](caminho/para/imagem_parte8_2.png)

---

## Parte 9 - Autorizando o DHCP no Active Directory (Etapa 1)

No topo do **Server Manager**, foi clicado no ícone da **bandeira com alerta amarelo** e selecionado **Complete DHCP configuration**.

![Print - Autorização DHCP 1](caminho/para/imagem_parte9_1.png)

---

## Parte 9 - Autorizando o DHCP no Active Directory (Etapa 2)

Na janela que se abriu, foi selecionado **Next**.

Em **Authorization**, certificou-se de que a opção **"Use the following user's credentials"** estava selecionada com o usuário `LAB\Administrator`.

Foi selecionado **Commit**.

Verificou-se que o status de ambas as etapas aparecia como **"Done"**.

E foi selecionado **Close**.

![Print - Autorização DHCP 2](caminho/para/imagem_parte9_2.png)
