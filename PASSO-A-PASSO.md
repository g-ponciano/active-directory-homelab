[Projeto 1 - Laboratório de Redes e Suporte.txt](https://github.com/user-attachments/files/31930667/Projeto.1.-.Laboratorio.de.Redes.e.Suporte.txt)
Projeto 1 - Laboratório de Redes e Suporte



1Parte 1 - Configurações Iniciais 1




<img width="945" height="723" alt="1Parte 1 - Configurações Iniciais 1" src="https://github.com/user-attachments/assets/5ce97fe2-ef5d-41d7-be6b-a22da862d80a" />




Após terminar a instalação do VirtualBox, o download das ISOs do Windows Server 2022 e Windows 11 e habilitar a virtualização do processador, foram realizadas as primeiras configurações da VM.

Foi mudado o nome para "DC01"

Carregado as ISOs dos sistemas operacionais

E alocado a quantidade correta de memória RAM (4096), número de processadores(2) e quantidade de espaço em disco a ser usado(40Gb).



2Parte 1 - Configurações iniciais 2

<img width="1919" height="1029" alt="2Parte 1 - Configurações iniciais 2" src="https://github.com/user-attachments/assets/217199ff-0325-4264-908d-efa3c4bf392a" />

Essa tela mostra a maioria das configurações antes citadas, a VM configurada e pronta para iniciar.



3Parte 2 - Configurando a rede

<img width="1919" height="1027" alt="3Parte 2 - Configurando a rede" src="https://github.com/user-attachments/assets/11928cf1-1844-4bed-924b-e2e0cb82bb84" />

Aqui foram feitas configurações de Rede da VM. 

"Ligado a" foi alterado para "Rede Interna" para isolar completamente o ambiente de testes da rede física local e da internet, evitando que o servidor DHCP do laboratório gere conflitos com a rede do computador hospedeiro.

"Nome" foi alterado para "LAB_REDE".




4Parte 4 - Instalando o Windows Server 2022

<img width="624" height="471" alt="4Parte 3 - Instalando o Windows Server 2022" src="https://github.com/user-attachments/assets/05687d08-70dd-4dd7-ad66-33898af0d020" />


A escolha da versão do Windows Server.

Nesse caso a escolha foi "Windows Server 2022 Datacenter Evaluation (Desktop Experience)", essa opção foi escolhida para garantir a instalação da interface gráfica, já que as opções sem essa marcação instalam o modo Server Core, que roda apenas via terminal de linha de comando.

Após finalizar a instalação do sistema, foi escolhida a senha para o sistema.



5Parte 5 - Server Manager 1

<img width="1920" height="1009" alt="5Parte 4 - Server Manager" src="https://github.com/user-attachments/assets/14083d0c-cdc9-4e93-b3a7-d6e28efa3f0d" />

Aqui foi dado o início a configuração do Server Manager, começando pela definição de um IP estático e confirmação do nome da máquina. 

Para o nome do computador foi definido "DC01"

E a descrição "Lab Server".



6Parte 5 - Server Manager 2

<img width="1920" height="1009" alt="6Parte  4 - Server Manager 2" src="https://github.com/user-attachments/assets/0c4e63c8-f871-4563-9b6d-39df117944b6" />

A definição do IP estático foi a seguinte:

IP address: 192.168.10.1

Subnet mask: 255.255.255.0

Default gateway: Deixado em branco.

Preferred DNS server: 127.0.0.1 (apontando para ele mesmo).



7Parte 5 - Active Directory 1

<img width="1920" height="1009" alt="7Parte 5 - Active Directory" src="https://github.com/user-attachments/assets/a529d95e-4063-4fb1-b112-bde7fb1acedc" />

Para a instalação do Active Directory foram adicionadas funções e recursos (Add roles and features).

Em Server Roles foi marcada a caixa "Active Directory Domain Services".

E após isso, foi aberta uma janela pop-up perguntando sobre os recursos adicionais.

A opção "Add Features" foi selecionada.



8Parte 5 - Active Directory 2

<img width="1920" height="1009" alt="8Parte 5 - Active Directory 2" src="https://github.com/user-attachments/assets/95439e7c-c241-4bde-b284-df3eff73557a" />

Tela de conclusão de instalação do Active Directory.



9Parte 6 - Promoção do Servidor 1

<img width="1920" height="1009" alt="9Parte 6 - Promoção do Servidor 1" src="https://github.com/user-attachments/assets/36ef54c8-907c-4059-b650-8f587d9a5057" />

Após instalado o Active Directory foi iniciada a promoção do servidor.

Em Deployment Configuration foi selecionada a opção "Add a new forest".

No campo Root domain name, foi digitado: lab.local.

E clicado em "Next".



10Parte 6 - Promoção do Servidor 2

<img width="1920" height="1009" alt="10Parte 6 - Promoção do Servidor 2" src="https://github.com/user-attachments/assets/d708f05f-94be-4b1e-811d-4b64b3ce7f3a" />

Em "Domain Controller Options" foi mantido os níveis funcionais em Windows Server 2016 (padrão).

foi definida uma senha para o DSRM (Directory Services Restore Mode).

E clicado em "Next".



11Parte 6 - Promoção do Servidor 3

<img width="1920" height="1009" alt="11Parte 6 - Promoção do Servidor 3" src="https://github.com/user-attachments/assets/16785b1e-6092-4eec-ab51-5e5254bb3b9f" />

Em "DNS Options" houve um aviso amarelo informando "A delegation for this DNS server cannot be created...",

Nesse caso foi ignorada por ser um aviso normal, pois é o primeiro servidor DNS da rede.

Foi selecionado "Next".



12Parte 6 - Promoção do Servidor 4

<img width="1920" height="1009" alt="12Parte 6 - Promoção do Servidor 4" src="https://github.com/user-attachments/assets/8f356ba3-8924-48d6-8c14-936a3c858082" />

Em Additional Options foi mantido o nome NetBIOS pré-preenchido, nesse caso "LAB" e selecionado "Next".

Foi selecionado "Next" na tela de "Paths".

E em "Review Options".



13Parte 6 - Promoção do Servidor 5

<img width="1920" height="1009" alt="13Parte 6 - Promoção do Servidor 5" src="https://github.com/user-attachments/assets/7e32e4c2-9dda-4104-a65b-c0806ead1d94" />

Em "Prerequisites Check",  o assistente fez uma verificação de pré-requisitos.
Após surgir a mensagem com ícone verde no topo (All prerequisite checks passed successfully) foi selecionado "Install".



14Parte 7 - Unidade Organizacional 1

<img width="1920" height="1009" alt="14Parte 7 - Unidade Organizacional 1" src="https://github.com/user-attachments/assets/8219596b-cca4-4cfb-8351-3fb1b86c66a7" />

Para criar a unidade organizacional foi aberta a ferramenta de gerenciamento do AD.

No Server Manager, foi selecionado no menu superior Tools, "Active Directory Users and Computers"

Na janela aberta, foi expandida a seta ao lado do domínio "lab.local" no painel esquerdo.

Foi clicado com o botão direito em cima de "lab.local" 

E depois foi selecionado "New" e "Organizational Unit."

foi digitado o nome: "LAB_Empresa" e certificado de que a opção "Protect container from accidental deletion" estava marcada.

Foi selecionado "OK", e assim foi criada a primeira pasta da Unidade Organizacional.



15Parte 7 - Unidade Organizacional 2

<img width="1920" height="1009" alt="15Parte 7 - Unidade Organizacional 2" src="https://github.com/user-attachments/assets/014fdd22-241a-41d5-8d80-4390159fdd0c" />

Agora foram criadas duas sub-pastas dentro dela:

Foi clicado com o botão direito em LAB_Empresa.

Depois foram selecionados "New" e "Organizational Unit"

E digitado: "Usuários".

Foi repetido o mesmo processo para criação de outra sub-pasta nomeada "Computadores".

Para criar o primeiro Usuário do Domínio, foi clicado com o botão direito dentro da sub-pasta "Usuários".

Foi selecionado "New" e depois "User".

Foram preenchidos os campos de identificação:

"First name: Mario" e "Last name: Silva" (Nome fictício).

"User logon name: mario.silva" foi definido como login de acesso.

Foi selecionado "Next".



16Parte 7 - Unidade Organizacional 3

<img width="1920" height="1009" alt="16Parte 7 - Unidade Organizacional 3" src="https://github.com/user-attachments/assets/c15477b5-53bb-4ff1-bb58-1d3576f9d671" />

Na tela de senha foi digitada uma senha forte.

Foi desmarcada a opção "User must change password at next logon".

Foi marcada a opção "Password never expires" para facilitar o laboratório.

Foi selecionado "Next" e "Finish".

Com isso, o usuário mario.silva@lab.local já existe no banco de dados e poderá ser usado para fazer login na máquina cliente (Windows 11) assim que for integrado a rede.



17Parte 8 - Instalando a Função de Servidor DHCP

<img width="1920" height="1009" alt="17Parte 8 - Instalando a Função de Servidor DHCP 1" src="https://github.com/user-attachments/assets/c68f2e8c-49b8-41c8-8995-d487613586f3" />

No Server Manager, foi selecionado "Manage" e, após isso "Add Roles and Features".

Foi selecionado "Next" nas telas iniciais até chegar em "Server Roles".

A caixa "DHCP Server" foi marcada.

Na janela pop-up que apareceu, foi selecionado "Add Features" e depois "Next".



18Parte 8 - Instalando a Função de Servidor DHCP 2

<img width="1920" height="1009" alt="18Parte 8 - Instalando a Função de Servidor DHCP 2" src="https://github.com/user-attachments/assets/1c89ec4f-4d90-430f-8c42-85e3f6aebe03" />

Foi selecionado "Next" nas telas de "Features" e "DHCP Server", até chegar a tela de "Confirmation" onde foi selecionado "Install".

Após a conclusão da instalação foi selecionado "Close".



19Parte 9 - Autorizando o DHCP no Active Directory

<img width="1920" height="1009" alt="19Parte 9 - Autorizando o DHCP no Active Directory 1" src="https://github.com/user-attachments/assets/dba579d2-fdf0-4abe-a54c-661d6f654a18" />

No topo do Server Manager, foi clicado no ícone da "bandeira com alerta amarelo" e selecionado "Complete DHCP configuration".



20Parte 9 - Autorizando o DHCP no Active Directory

<img width="1920" height="1009" alt="20Parte 9 - Autorizando o DHCP no Active Directory 2" src="https://github.com/user-attachments/assets/c888cb8b-0147-4f2a-bd2c-c9bec2c8b800" />

Na janela que abriu, foi selecionado "Next".

Em Authorization, foi certificado de que a opção "Use the following user's credentials" estava selecionada com o usuário "LAB\Administrator".

Foi selecionado "Commit".

Verificou-se que o status de ambas as etapas aparecia como "Done".

E foi selecionado "Close".



21Parte 10 - Criando o Escopo de IPs (DHCP Scope)

<img width="1920" height="1009" alt="21Parte 10 - Criando o Escopo de IPs (DHCP Scope)" src="https://github.com/user-attachments/assets/ad15ef1b-cb09-4144-9214-fa3df6f6359c" />

No menu superior do Server Manager, foi selecionado "Tools" e "DHCP".

No painel esquerdo, foi expandido o nome do servidor "(dc01.lab.local)".

Foi clicado com o botão direito sobre a opção "IPv4".

E selecionado "New Scope....".

Foi selecionado "Next" no assistente.

Em "Name" foi digitado "LAB_SCOPE".

E selecionado "Next".



22Parte 10 - Criando o Escopo de IPs (DHCP Scope) 2

<img width="1920" height="1009" alt="22Parte 10 - Criando o Escopo de IPs (DHCP Scope) 2" src="https://github.com/user-attachments/assets/959da2cd-6933-4e48-919f-2234e60c7df9" />

"IP Address Range" foi preenchido com a faixa da rede:

Start IP address: 192.168.10.100

End IP address: 192.168.10.200

Length: 24

Subnet mask: 255.255.255.0

Foi selecionado "Next".



23Parte 10 - Criando o Escopo de IPs (DHCP Scope) 3

<img width="1920" height="1009" alt="23Parte 10 - Criando o Escopo de IPs (DHCP Scope) 3" src="https://github.com/user-attachments/assets/d95f24db-16e0-4eb8-b001-38804523adc4" />

Em "Add Exclusions and Delay" não foi preciso excluir nada dentro da faixa 100-200.

Foi selecionado "Next".

Para "Lease Duration" foi mantido o padrão de 8 dias

E selecionado "Next".

Em "Configure DHCP Options" clicado em "Next".

Em "Router (Default Gateway)" como a rede do projeto é isolada e não tem roteador, foi apenas selecionado "Next" sem preencher.

Os campos de "Domain Name and DNS Servers" foram preenchidos da seguinte forma:

Parent domain: lab.local

IP address: 192.168.10.1

E foi selecionado "Add", o nome será resolvido para "dc01.lab.local".

Após "Add" ser selecionado apareceu o seguinte aviso "The IP Adress 192.168.10.1 is not a valid DNS adress, do you still want to add it ?", esse aviso aparece porque o assistente do DHCP tenta enviar uma consulta de teste para o IP 192.168.10.1 para confirmar se ele responde como DNS. Como o servidor está em uma rede interna isolada sem internet, a validação automática falha e exibe esse alerta

Na caixa de diálogo aberta foi selecionado "Yes".



24Parte 10 - Criando o Escopo de IPs (DHCP Scope) 4

<img width="1920" height="1009" alt="24Parte 10 - Criando o Escopo de IPs (DHCP Scope) 4" src="https://github.com/user-attachments/assets/deaf389e-f049-42a0-8090-658463835eb3" />

Foi clicado em cima do IP "192.168.0.1"

E no botão "Remove" ao lado.

Apenas o IP "192.168.10.1" permaneceu na lista.

Foi selecionado "Next" para continuar a configuração do escopo.

"WINS Servers" foi deixado em branco

E selecionado "Next".

Activate Scope foi clicado em "Finish".



25Parte 11 - Criação da Máquina Cliente (Windows 11)

<img width="784" height="527" alt="25Parte 11 - Criação da Máquina Cliente" src="https://github.com/user-attachments/assets/f1ce46bc-3a0f-4fd8-9597-be8e72fde0c3" />

Aqui as configurações foram praticamente as mesmas da criação do Servidor (Windows Server 2022), as únicas diferenças foram:

VM Name: PC01

E a desmarcação da opção "Proceed with Unattended Installation". Eembora a instalação automatizada funcione bem no Windows Server, no Windows 11 do VirtualBox ela costuma gerar pequenos problemas:

Criação de usuário genérico: O VirtualBox tenta criar automaticamente uma conta chamada "vboxuser" com senha padrão, o que pode causar confusão depois na hora de fazer o login local.
Bugs na finalização: É comum o script automatizado do VirtualBox travar ou entrar em loop na tela de preparação inicial (OOBE) do Windows 11.

Ao realizar a instalação manual tradicional:

Você evita falhas de scripts do VirtualBox.
Você cria seu próprio usuário local temporário (ex: adminlocal).
O processo de instalação segue o padrão exato de um computador físico corporativo.



26Parte 12 - Configurando a Rede da Máquina Cliente

<img width="901" height="486" alt="26Parte 12 - Configurando a Rede da Máquina Cliente" src="https://github.com/user-attachments/assets/9fb55913-18e5-4974-9339-4b371c0b8c59" />

Antes de ligar a VM, é necessário colocá-la no mesmo segmento de rede virtual do "DC01" (Servidor):

A VM "PC01" foi selecionada.

E em seguida foi clicado em "Configurações" e "Rede".

Na aba Placa 1 foram definidos os seguintes parâmetros:

Ligado a: Rede Interna.

Nome: LAB_REDE (pois deve ser o mesmo nome usado no servidor).

Foi selecionado "OK".



27Parte 13 - Validando o IP no Cliente






No PC01, foi aberto o menu "Iniciar", 

Digitado "cmd e aberto o "Prompt de Comando".

Foi digitado o seguinte comando, "ipconfig /all".

E apertado "Enter".



28Parte 14 - Voltando o PC01 para IP Automático (DHCP) 1



No PC01, foi pressionado "Win + R".

Digitado "ncpa.cpl"

E apertado "Enter".

Foi clicado com o botão direito em "Ethernet", "Propriedades" e dado duplo clique em "Protocolo IP Versão 4 (TCP/IPv4)".

Foram marcadas as duas opções para automático:

"Obter um endereço IP automaticamente" e "Obter o endereço dos servidores DNS automaticamente".

E Clicado em "OK" e "OK".



29Parte 14 - Voltando o PC01 para IP Automático (DHCP) 2



No Prompt de Comando (CMD) do PC01, foi executado o comando "ipconfig /renew".

Em seguida, foi o comando "ipconfig /all". 

Confirmando o recebimento do IP "192.168.10.100".

E o DNS Server "192.168.10.1".



30Parte 15 - Testando a Resolução do Domínio (DNS) 1



No CMD do PC01, foi executado "nslookup lab.local".

O comando retornou o nome do servidor e o endereço "192.168.10.1".



31Parte 15 - Testando a Resolução do Domínio (DNS) 2



No PC01, foi pressionado "Win + R".

Digitado "sysdm.cpl".

E pressionado "Enter", o que abrirá as "Propriedades do Sistema".

Na aba "Nome do Computador", foi selecionado o botão "Alterar"... (Change...).

Na seção "Membro de" foi selecionado a opção "Domínio" (Domain).

E digitado "lab.local".

E clicado em "OK".



32Parte 15 - Testando a Resolução do Domínio (DNS) 3



A mensagem "Sign in to: LAB" logo abaixo do campo de senha confirma que a máquina já está autenticando diretamente ao servidor "Active Directory".



33Parte 16 - Criando grupos



Na VM do DC01, foi pressionado "Win + R".

Digite "dsa.msc".

E pressionado "Enter".

Na árvore do lado esquerdo, foi expandido o domínio "lab.local".

Foi clicado com o botão direito em "Usuarios".

Em seguida em "Novo" (New) e "Grupo" (Group).

Agora, para criar o Grupo "TI".

Na janela "Novo Objeto - Grupo" (New Object - Group), foram preenchidos os seguintes dados:

Group name: TI

Group scope: Global

Group type: Security

E clicado em "OK".

Foi repetido o mesmo Processo para os demais grupos: "RH, Financeiro e Suporte" mantendo o "Group scope: Global" e "Group type: Security".



34Parte 17 - Adicionando o Usuário ao Grupo



Para vincular o usuário "mario.silva" ao grupo "TI", foi clicado com o botão direito no grupo "TI".

E selecionado "Propriedades (Properties)".

Na aba "Membros (Members)" foi clicado em "Adicionar... (Add...)".

Foi digitado "mario.silva".

Clicado em "Verificar Nomes (Check Names)".

Depois em "OK".

E finalmente "Aplicar" e "OK".



35Parte 18 - Implementando o File Server



Para criar a estrutura de pastas no DC01, foi aberto o "Explorador de Arquivos (File Explorer)".

E navegado até "C:\".

Foi criada uma pasta chamada "Compartilhamento".

Foi entrado na pasta "C:\Compartilhamento" e criado três subpastas:

TI

RH

Financeiro



36Parte 19 - Compartilhando a Pasta Principal na Rede



Foi clicado com o botão direito na pasta "C:\Compartilhamento"

E selecionado "Properties (Propriedades)".

Na aba "Sharing (Compartilhamento)" foi clicado em "Advanced Sharing... (Compartilhamento Avançado...)".

Foi marcada a caixa "Share this folder (Compartilhar esta pasta)".

Foi clicado no botão "Permissions (Permissões)".

Foi garantido que o grupo "Everyone (Todos)" tenha permissão de "Full Control (Controle Total)" ou "Change (Alteração)".

Nota de arquitetura: No Windows Server, liberamos o acesso de rede na pasta raiz e controlamos quem pode fazer o que através da aba "Security (NTFS)" nas subpastas.

Foi clicado em "OK", "OK" e fechada a janela.



37Parte 20 - Configurando Permissões da Pasta TI (Quebra de Herança)



Foi clicado com o botão direito na pasta "C:\Compartilhamento\TI" 

E selecionado "Properties (Propriedades)".

Na aba "Security (Segurança)" foi clicado no botão "Advanced (Avançado)".

Na parte inferior, foi clicado em "Disable inheritance (Desabilitar herança)".

Foi selecionada a opção "Convert inherited permissions into explicit permissions... (Converter permissões herdadas em permissões explícitas...)".

Foi selecionado o grupo genérico "Users (Usuários)" da lista.

E clicado em "Remove (Remover)".

Foi clicado em "OK" para voltar à tela anterior.



38Parte 21 - Adicionando os Grupos e Definindo Permissões 1



Ainda na aba "Security" da pasta TI.

Foi clicado em "Edit... (Editar...)" para definir os acessos para o Grupo TI (Acesso de Modificação):

Foi clicado em "Add... (Adicionar...)".

Digitado "TI".

Clicado em "Check Names" e dado "OK".



39Parte 22 - Adicionando os Grupos e Definindo Permissões 2



Foi marcada a caixa "Modify (Modificar)" na coluna "Allow (Permitir)".

Clicado em "Apply" e dado "OK".



40Parte 23 - Adicionando os Grupos e Definindo Permissões 3



Para o Grupo "RH (Acesso de Leitura)":

Foi clicado em "Add... (Adicionar...)".

Digitado "RH"

Clicado em "Check Names" e dado "OK".



41Parte 23 - Adicionando os Grupos e Definindo Permissões 4



Foram mantidas apenas as caixas de "Read & execute" e "Read (Leitura)" marcadas.

Grupo Financeiro (Sem Acesso):

No modelo de segurança do Windows não foi adicionado o grupo "Financeiro" à lista pois, a ausência do grupo na lista garante automaticamente o "acesso negado (No access)".

Foi clicado em "Apply" e "OK".



42Parte 24 - Testando o Acesso no PC01 1



No PC01 (logado com o usuário mario.silva).

Foi pressionado "Win + R"

Digitado o caminho da rede do servidor, "\\DC01\Compartilhamento".

E apertado "Enter":



43Parte 24 - Testando o Acesso no PC01 2



Como o Mário pertence ao grupo "TI", foi feita a tentativa de criar um arquivo de texto dentro dela porém o aviso "Network Error" foi mostrado. Esse erro acontece por um detalhe muito comum no Active Directory: o Windows só carrega os novos grupos de um usuário no momento em que ele faz o login. Como o Mário já estava logado no "PC01" quando foi adicionado ao grupo "TI" no servidor, a máquina cliente ainda não recebeu essa permissão.



43Parte 24 - Testando o Acesso no PC01 3

Para resolver esse problema foi feito logoff e login novamento no "PC01".

Para validar o "Token de Segurança" no PC01 após fazer login novamente foi aberto o "Prompt de Comando (CMD)" no PC01.

E executado "whoami /groups".

Foi conferido se o grupo "LAB\TI" apareceu listado no resultado, porém não apareceu o que significa que o "Kerberos (sistema de autenticação do Windows)" ainda não emitiu um novo bilhete de segurança com a lista de grupos atualizada para o Mário.



44Parte 24 - Testando o Acesso no PC01 4



Para resolver esse problema foram seguidos os passos abaixo:



Passo 1 - Verificando a Associação no DC01:



No servidor voltou-se a VM do DC01.

Foi aberto o "Active Directory (dsa.msc)".

Em seguida foi selecionado "LAB_Empresa" e "Usuários" 

E dado um duplo clique no usuário "Mario Silva".

Foi clicado na aba "Member Of (Membro de)".

E confirmado se o grupo "TI" está realmente aparecendo nessa lista.

Como não estava, foi clicado em "Add...".

Digitado "TI".

Clicado em "Check Names".

E dado "OK".

Depois foi clicado em "Apply" e "OK".



46Parte 24 - Testando o Acesso no PC01 5



Passo 2 - Fazendo Logoff Completo no PC01:



Na máquina cliente, o Windows só reconstrói a lista de grupos durante um "logoff real" (bloquear a tela ou reiniciar sem encerrar a sessão não atualiza os tokens em cache imediatamente).

No PC01, foi clicado no menu "Iniciar".

Clicado no ícone do usuário "mario.silva".

E escolhido "Sign out (Sair)".

Na tela de login, entrou-se novamente com a conta "mario.silva" e a senha.



Passo 3 - Validar novamente no CMD:

Na máquina cliente foi aberto o Prompt de Comando (CMD) normal.

Digitado o comando "whoami /groups" novamente.

O grupo LAB\TI agora apareceu listado no meio do resultado.



47Parte 24 - Testando o Acesso no PC01 6



Foi aberto novamente o caminho "\\DC01\Compartilhamento\TI" pelo "Executar (Win + R)".

E criado um "Text Document (Documento de Texto)", dessa vez sem avisos.



48Parte 25 - Criando uma política simples com Group Policy 1



No DC01, foram pressionadas as teclas "Win + R".

Digitado "gpmc.msc" 

E pressionado "Enter".



49Parte 26 - Criando uma política simples com Group Policy 2



Para abrir o "Gerenciador de Diretivas de Grupo" na árvore da esquerda, foram expandidos os seguintes itens "Forest > lab.local > Domains > lab.local".

Foi clicado com o botão direito em "Default Domain Policy" 

E selecionado "Edit... (Editar...)".

Para "Localizar as Configurações de Senha" no "Group Policy Management Editor" na janela do editor que se abriu, foi navegado pela árvore no lado esquerdo até o seguinte caminho:

Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy.

Para "Configurar o Tamanho Mínimo e Complexidade da Senha" na pasta "Password Policy" foi clicado duas vezes sobre "Minimum password length".

Foi marcada a caixa "Define this policy setting".

Alterado o valor para 8 (caracteres).

E clicado em "OK".



50Parte 26 - Criando uma política simples com Group Policy 3



Em relação a "Complexidade de Senha" foi clicado duas vezes sobre "Password must meet complexity requirements".

Foi marcada a caixa "Define this policy setting".

Selecionado "Enabled (Habilitado)" para exigir letras maiúsculas, minúsculas e números/símbolos.

E clicado em "OK".



51Parte 27 - Testando a Política de Senhas 1



Foi pressionado "Win + R".

Depois digitado "dsa.msc".

Pressionado "Enter".

E foi navegado até a OU onde está o usuário de teste, "lab.local > LAB_Empresa > Usuários".

Agora foi realizado o teste para redefinir a senha para uma senha fraca, foi clicado com o botão direito sobre o usuário "Mario Silva".

E escolhido "Reset Password... (Redefinir senha...)".

Foi digitada uma senha que não atendia aos requisitos e desmarcada a opção "User must change password at next logon", para facilitar o teste.

Foi clicado em "OK".



52Parte 27 - Testando a Política de Senhas 2



Resultado: O Windows Server exibiu uma mensagem de erro informando que a senha não cumpre os requisitos mínimos de tamanho ou complexidade da diretiva do domínio (The password does not meet the password policy requirements).



53Parte 27 - Testando a Política de Senhas 3



Agora foi feito o testa para redefinir para uma senha forte, foi clicado novamente com o botão direito no "Mario Silva > Reset Password....".

Foi digitada uma senha que atendeu a todos os requisitos.

E clicado em "OK".

Resultado: O Active Directory exibiu a mensagem de confirmação: "The password for Mario Silva has been changed."



54Parte 28 - Criando uma estrutura mais profissional 1



Para criar as "Unidades Organizacionais (OUs) Principais" foi pressionado "Win + R"

Digitado "dsa.msc".

E pressionado "Enter".

Foi clicado com o botão direito no nome do domínio "lab.local".

Foi selecionado "New (Novo) > Organizational Unit (Unidade Organizacional)".

Digitado "TI".

E clicado em "OK".



55Parte 28 - Criando uma estrutura mais profissional 2



Para "Criar as Sub-OUs em Cada Departamento" foi clicado com o botão direito na OU "TI > New > Organizational Unit".

Foi nomeada como "Usuários".

E clicado em "OK".

Foi clicado com o botão direito novamente na OU "TI > New > Organizational Unit".

Foi nomeie como "Computadores".

E clicado em "OK".

Foi repetida essa subcriação "Usuarios e Computadores" dentro de "RH, Financeiro e Suporte".



56Parte 28 - Criando uma estrutura mais profissional 3



Para mover os "Objetos Existentes para os Novos Locais" como o "Usuário: Mario Silva", foi clicado nele com o botão direito.

E depois em "Move... (Mover...)".

E selecionado o caminho "lab.local > TI > Usuários".



57Parte 28 - Criando uma estrutura mais profissional 4



Para Mover o Computador foi clicado com o botão direito no computador "PC01".

Depois em "Move...".

E selecionado "lab.local > TI > Computadores".

Com isso, o Active Directory ficou profissional e pronto para receber GPOs direcionadas a setores específicos.



58Parte 29 - Criando mais usuários no Active Directory 1



Para criar mais usuários no Active Directory, no "DC01", foi aberto o "Active Directory Users and Computers (dsa.msc)".

Foi navegado até a OU de destino, "lab.local > RH > Usuarios".

Foi clicado com o botão direito na pasta "Usuarios > New (Novo) > User (Usuário)".

Foi preenchido os campos:

First name: Maria

User logon name: maria

E clicado em "Next".



59Parte 29 - Criando mais usuários no Active Directory 2



Para definir a senha e regras, no "DC01", foi digitado uma senha forte, foi desmarcado "User must change password at next logon (O usuário deve alterar a senha no próximo logon)".

Foi marcado "Password never expires (A senha nunca expira)" para facilitar os testes do laboratório.

Foi clicado em "Next".

E depois em "Finish".



60Parte 29 - Criando mais usuários no Active Directory 3



Para adicionar o usuário ao grupo de segurança, no "DC01", foi clicado com o botão direito sobre o usuário "Maria", e escolhido "Properties (Propriedades)".

Foi acessada a aba "Member Of (Membro de)".

E clicado em "Add....".

Foi digitado "RH".

Foi clicado em "Check Names".

E dado "OK".

Por fim, foi clicado em "Apply" e "OK".



61Parte 29 - Criando mais usuários no Active Directory 4



Foi repetido o processo para os outros dois usuários:

João: Foi criado em "Financeiro > Usuários", com "login joao".

E adicionado ao grupo "Financeiro".

Maria: Foi criada em "Suporte > Usuarios", com "login maria".

E adicionada ao grupo "Suporte".



62Parte 30 - Criando a GPO de Mapeamento de Rede 1

No "DC01", foi aberto o "Group Policy Management (Win + R > gpmc.msc)".

E clicado com o botão direito sobre a raiz do domínio "lab.local > Create a GPO in this domain, and Link it here....".

A GPO foi nomeada como "GPO - Mapeamento Disco Z.

E clicado em "OK".



63Parte 30 - Criando a GPO de Mapeamento de Rede 2



Foi clicado com o botão direito na GPO criada e selecionado "Edit... (Editar)".

Para configurar a unidade mapeada, no "Editor de GPO", foi navegado pela árvore no painel esquerdo, "User Configuration > Preferences > Windows Settings > Drive Maps".

Foi clicado com o botão direito no painel direito, "New > Mapped Drive".

Foi preenchida a janela de configuração:

Action: Update

Location: \\DC01\Compartilhamento

Drive Letter: Z

Label as: Arquivos da Empresa

E finalmente clicado em "Apply" e "OK".



64Parte 30 - Criando a GPO de Mapeamento de Rede 3



Para testar no cliente, no "PC01" foi aberto o "CMD " e executado "DOSgpupdate /force".



65Parte 30 - Criando a GPO de Mapeamento de Rede 4



Para a confirmação da criação do disco de rede foi aberto o "File Explorer (Este Computador / This PC)".

E foi verificado que o disco de rede "Arquivos da Empresa (Z:)" surgiu automaticamente.

Ao clicar duas vezes no disco Z:, o sistema aplicará de forma transparente a mesma regra de acesso NTFS que você acabou de validar: cada usuário só conseguirá acessar ou alterar as pastas às quais tem direito.















