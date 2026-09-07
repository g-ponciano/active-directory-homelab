# 🖥️ Homelab: Infraestrutura Corporativa no Windows Server, Active Directory & GPOs

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Windows 11](https://img.shields.io/badge/Windows%2011-Enterprise-0078D4?style=for-the-badge&logo=windows11&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-AD%20DS-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)

---

## 📌 Visão Geral do Projeto

Este laboratório prático (*Homelab*) teve como objetivo projetar, implantar, estruturar e validar uma infraestrutura de rede corporativa completa baseada em ecossistema Microsoft. 

O projeto contempla desde a instalação e promoção de um **Domain Controller (DC)** até a implementação de gestão centralizada de identidades, automação via **Group Policy Objects (GPO)**, servidor de arquivos com **matriz de permissões NTFS granular** e validação funcional de ponta a ponta em uma estação cliente com Windows 11.

---

## 📐 Arquitetura & Topologia da Rede

```text
                                  ┌────────────────────────┐
                                  │   Domínio: lab.local   │
                                  └───────────┬────────────┘
                                              │
                      ┌───────────────────────┴───────────────────────┐
                      │                                               │
           ┌──────────▼──────────┐                         ┌──────────▼──────────┐
           │     Servidor DC01   │                         │    Estação PC01     │
           ├─────────────────────┤                         ├─────────────────────┤
           │ OS: Windows Server  │                         │ OS: Windows 11 Ent  │
           │ IP: 192.168.10.10/24│                         │ IP: DHCP Dinâmico   │
           │ Roles: AD DS, DNS,  │                         │ Rol: Cliente do     │
           │        DHCP, FS     │                         │      Domínio        │
           └─────────────────────┘                         └─────────────────────┘
### Detalhes de Endereçamento:
* **Domínio Active Directory:** `lab.local`
* **Sub-rede Interna:** `192.168.10.0/24`
* **Domain Controller (DC01):** `192.168.10.10` (IP Estático)
* **Escopo DHCP:** `192.168.10.100` até `192.168.10.200`
* **DNS Primário:** `192.168.10.10` (Integrado ao AD DS)

---

## ⚙️ Implementações Técnicas

### 1. Serviços Essenciais de Infraestrutura
* **AD DS (Active Directory Domain Services):** Instalação e promoção do servidor `DC01` a Controlador de Domínio do ambiente `lab.local`.
* **DNS Server:** Configuração de zonas de pesquisa direta e reversa integradas ao AD para resolução de nomes do ambiente.
* **DHCP Server:** Configuração de escopo dinâmico com distribuição automática de IP, Máscara, Gateway e ponteiro DNS do domínio para as estações clientes.

---

### 2. Gestão de Identidades (OUs, Grupos e Usuários)
Estruturação hierárquica baseada em divisões setoriais da empresa para facilitar a aplicação de políticas corporativas.

```text
lab.local
 ├── 📁 TI
 │    ├── 📁 Usuarios (Ex: Mário Silva, Guilherme)
 │    └── 📁 Computadores (Ex: PC01)
 ├── 📁 RH
 │    ├── 📁 Usuarios (Ex: Maria)
 │    └── 📁 Computadores
 ├── 📁 Financeiro
 │    ├── 📁 Usuarios (Ex: João)
 │    └── 📁 Computadores
 └── 📁 Suporte
      ├── 📁 Usuarios
      └── 📁 Computadores
```
* **Grupos Globais de Segurança:** Criados para cada departamento (`TI_Grupo`, `RH_Grupo`, `Financeiro_Grupo`, `Suporte_Grupo`).
* **Atribuição de Acesso:** Usuários atribuídos estritamente aos seus respectivos grupos setoriais.

---

### 3. Automação e Segurança com Diretivas de Grupo (GPO)
* **Política Global de Senhas:** Aplicação de regras rígidas de complexidade (mínimo de 8 caracteres, maiúsculas, minúsculas, números e símbolos).
* **Mapeamento Automático de Rede (Disco Z:):**
  * Configuração de GPO para mapear o diretório `\\DC01\Compartilhamento` como unidade física **`Z:`** diretamente no Windows Explorer dos usuários no momento do logon.

---

### 4. Servidor de Arquivos & Matriz de Permissões NTFS
Implementação de compartilhamento centralizado com **desabilitação de herança de permissões** na pasta raiz e aplicação do princípio do menor privilégio (*Least Privilege*):

| Pasta Compartilhada | Grupo de Segurança | Permissão NTFS Aplicada | Justificativa / Comportamento |
| :--- | :--- | :--- | :--- |
| `\\DC01\Compartilhamento\TI` | `TI_Grupo` | **Modify (Modificar)** | Controle total de leitura, gravação e exclusão para a equipe de TI. |
| `\\DC01\Compartilhamento\RH` | `TI_Grupo` | **Read & Execute (Leitura)** | Permite que a TI consulte documentações sem alterar dados do RH. |
| `\\DC01\Compartilhamento\Financeiro` | `TI_Grupo` | **Access Denied (Bloqueado)** | Bloqueio explícito/implícito de acesso a dados confidenciais. |
| `\\DC01\Compartilhamento\Financeiro` | `Financeiro_Grupo` | **Modify (Modificar)** | Acesso restrito e exclusivo para membros do departamento financeiro. |

---

## 🧪 Matriz de Testes & Homologação

Para garantir a estabilidade e segurança da infraestrutura, os seguintes testes de validação foram executados com sucesso na estação **PC01**:

| Item Testado | Comando / Procedimento | Resultado Esperado | Status |
| :--- | :--- | :--- | :---: |
| **Atribuição IP** | `ipconfig /all` | Receber IP da faixa `192.168.10.x` via DHCP | **APROVADO** |
| **Resolução DNS** | `nslookup lab.local` | Retornar IP `192.168.10.10` do DC01 | **APROVADO** |
| **Ingresso no Domínio** | `systeminfo` | Estação associada ao domínio `lab.local` | **APROVADO** |
| **Autenticação AD** | Logon com `mario.silva` | Login efetuado com sucesso no domínio | **APROVADO** |
| **GPO de Mapeamento** | `gpupdate /force` | Apresentação automática da unidade **(Z:)** em *Este Computador* | **APROVADO** |
| **Segregação NTFS (TI)** | Acessar pastas no **Disco Z:** | **TI:** Acesso Total \| **RH:** Apenas Leitura \| **Financeiro:** Acesso Negado | **APROVADO** |
| **Segregação NTFS (Fin.)** | Logon com `joao` | **Financeiro:** Acesso Total \| **TI:** Acesso Negado | **APROVADO** |

---

## 📸 Evidências do Ambiente


### 1. Estrutura de OUs no Active Directory (`DC01`)
<img width="1920" height="1009" alt="55Parte 28 - Criando uma estrutura mais profissional 2" src="https://github.com/user-attachments/assets/743ea156-173f-4324-8456-092eddff1674" />


### 2. Mapeamento Automático do Disco Z: no Cliente (`PC01`)
<img width="1920" height="1009" alt="63Parte 30 - Criando a GPO de Mapeamento de Rede 2" src="https://github.com/user-attachments/assets/41750485-43d4-4b2c-84dc-dc4c39efccd8" />


### 3. Validação de Acesso Negado (NTFS)
<img width="1920" height="1009" alt="43Parte 24 - Testando o Acesso no PC01 2" src="https://github.com/user-attachments/assets/bd6f1f66-34cf-46d3-8be8-25d6ceb44773" />


---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Hypervisor:** Oracle VirtualBox
* **Sistemas Operacionais:** Windows Server 2022 / Windows 11 Enterprise
* **Serviços de Rede:** AD DS, DNS Server, DHCP Server, File & Storage Services
* **Ferramentas de Gestão:** Administrative Center (ADAC), GPMC (`gpmc.msc`), CMD / PowerShell

---

## ✍️ Autor

Desenvolvido por **Guilherme Ponciano**  
*Profissional de Tecnologia da Informação com foco em Infraestrutura, Suporte Avançado e SysAdmin.*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/g-ponciano)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/g-ponciano)
