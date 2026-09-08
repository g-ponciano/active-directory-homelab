# Projeto 1 - Laboratório de Redes e Suporte

---

## Parte 1 - Configurações Iniciais (1)

Após terminar a instalação do VirtualBox, o download das ISOs do Windows Server 2022 e do Windows 11 e habilitar a virtualização do processador, foram realizadas as primeiras configurações da VM.

- Foi alterado o nome para **"DC01"**
- Carregadas as ISOs dos sistemas operacionais
- Alocada a quantidade correta de memória RAM (4096 MB), número de processadores (2) e quantidade de espaço em disco a ser usado (40 GB)

![Print - Configurações Iniciais 1](caminho/para/sua_imagem_01.png)

---

## Parte 1 - Configurações Iniciais (2)

Esta tela mostra a maioria das configurações citadas anteriormente, com a VM configurada e pronta para iniciar.

![Print - Configurações Iniciais 2](caminho/para/sua_imagem_02.png)

---

## Parte 2 - Configurando a Rede

Aqui foram feitas as configurações de rede da VM:

- **"Ligado a":** foi alterado para **"Rede Interna"** para isolar completamente o ambiente de testes da rede física local e da internet, evitando que o servidor DHCP do laboratório gere conflitos com a rede do computador hospedeiro.
- **"Nome":** foi alterado para **"LAB_REDE"**.

![Print - Configurando a Rede](caminho/para/sua_imagem_03.png)

---

## Parte 4 - Instalando o Windows Server 2022

A escolha da versão do Windows Server:

Neste caso, a escolha foi **"Windows Server 2022 Datacenter Evaluation (Desktop Experience)"**. Essa opção foi escolhida para garantir a instalação da interface gráfica, já que as opções sem essa marcação instalam o modo *Server Core*, que roda apenas via terminal de linha de comando.

Após finalizar a instalação do sistema, foi definida a senha para o sistema.

![Print - Instalando o Windows Server 2022](caminho/para/sua_imagem_04.png)

---

## Parte 5 - Server Manager (1)

Aqui foi dado início à configuração do Server Manager, começando pela definição de um IP estático e confirmação do nome da máquina:

- **Nome do computador:** `"DC01"`
- **Descrição:** `"Lab Server"`

![Print - Server Manager 1](caminho/para/sua_imagem_05.png)

---

## Parte 5 - Server Manager (2)

A definição do IP estático foi a seguinte:

- **IP address:** `192.168.10.1`
- **Subnet mask:** `255.255.255.0`
- **Default gateway:** *(Deixado em branco)*
- **Preferred DNS server:** `127.0.0.1` (apontando para ele mesmo)

![Print - Server Manager 2](caminho/para/sua_imagem_06.png)

---

## Parte 5 - Active Directory (1)

Para a instalação do Active Directory, foram adicionadas funções e recursos (*Add roles and features*).

Em **Server Roles**, foi marcada a caixa **"Active Directory Domain Services"**.

Após isso, foi aberta uma janela pop-up perguntando sobre os recursos adicionais, onde a opção **"Add Features"** foi selecionada.

![Print - Active Directory 1](caminho/para/sua_imagem_07.png)

---

## Parte 5 - Active Directory (2)

Tela de conclusão da instalação do Active Directory.

![Print - Active Directory 2](caminho/para/sua_imagem_08.png)

---

## Parte 6 - Promoção do Servidor (1)

Após a instalação do Active Directory, foi iniciada a promoção do servidor.

Em **Deployment Configuration**, foi selecionada a opção **"Add a new forest"**.

No campo **Root domain name**, foi digitado: `lab.local` e clicado em **"Next"**.

![Print - Promoção do Servidor 1](caminho/para/sua_imagem_09.png)

---

## Parte 6 - Promoção do Servidor (2)

Em **"Domain Controller Options"**, foram mantidos os níveis funcionais em Windows Server 2016 (padrão).

Foi definida uma senha para o DSRM (*Directory Services Restore Mode*) e clicado em **"Next"**.

![Print - Promoção do Servidor 2](caminho/para/sua_imagem_10.png)
