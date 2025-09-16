# Ferramentas de Gerenciamento e Implantação no Azure 

## 1. Introdução
O Azure oferece várias formas de **interagir, gerenciar e implantar recursos**.  
Todas elas conversam com o **Azure Resource Manager (ARM)**, o **plano de controle** que autentica/autoriz­a (Entra ID + RBAC), aplica **Azure Policy** e **Resource Locks**, orquestra **Resource Providers** e registra o **histórico de deployments**.

Na **AZ-900**, você precisa reconhecer **o que cada ferramenta é, para que serve e quando usar**.

---

## 2. Ferramentas de Gerenciamento (Interação com o Azure)

### 2.1 Azure Portal
- **O que é:** interface gráfica (GUI) no navegador.
- **Finalidade:** criar, configurar e monitorar recursos visualmente.
- **Vantagens:** intuitivo, sem instalação, excelente para começar e para troubleshooting.
- **Limitações:** pouca reprodutibilidade; sujeito a diferenças manuais.
- **Exemplo prático:** criar uma VM preenchendo formulários no Portal.

### 2.2 Azure Cloud Shell
- **O que é:** terminal no navegador (Portal do Azure ou `shell.azure.com`) com **Azure CLI** e **Azure PowerShell** pré-instalados.
- **Finalidade:** executar comandos sem instalar nada localmente.
- **Vantagens:** zero setup, acessível de qualquer lugar; armazenamento persistente via Azure Files.
- **Limitações:** requer internet; não acessa sua rede local.
- **Exemplo prático:** abrir o Cloud Shell e executar `az vm list`.

### 2.3 Azure PowerShell
- **O que é:** módulos **Az** para administrar o Azure via **scripts PowerShell**.
- **Finalidade:** automação administrativa, especialmente em ambientes Windows.
- **Vantagens:** trabalha com **objetos** (facilita automações complexas), integra bem com Windows/AD.
- **Exemplo de comandos:**
  ```powershell
  Connect-AzAccount
  New-AzResourceGroup -Name RG-Teste -Location eastus

### 2.4 Azure CLI
- **O que é:** ferramenta de linha de comando multiplataforma (`az`).  
- **Finalidade:** automação rápida, uso em pipelines DevOps, scripts em Linux/macOS/Windows.  
- **Vantagens:** simples, multiplataforma, saída em JSON (ótimo para integrar com outros scripts).  
- **Exemplo de comandos:**
  ```bash
  az login
  az group create --name RG-Teste --location eastus

  
## 3. Infraestrutura como Código (IaC) no Azure

### 3.1 Azure Resource Manager (ARM)
- **O que é:** plano de controle do Azure (tudo passa por ele: Portal, CLI, PowerShell, APIs, SDKs e Templates).  
- **Função:** valida **RBAC/Policy/Locks**, aciona **Resource Providers** (ex.: `Microsoft.Compute`, `Microsoft.Storage`) e registra o **deployment**.  
- **Benefícios:**
  - Consistência entre ferramentas.  
  - Idempotência (evita recriações desnecessárias).  
  - Governança centralizada (RBAC/Policy/Locks).  
  - Histórico de deployments (logs/outputs).  

---

### 3.2 ARM Templates (JSON)
- **O que é:** arquivos **JSON declarativos** que descrevem recursos, parâmetros, variáveis e dependências.  
- **Modelo declarativo:** você define o **estado desejado**; o ARM aplica as mudanças necessárias.  
- **Idempotente:** reaplicar o template não duplica recursos já corretos.  
- **Exemplo prático:** um template que cria **3 VMs + VNet + Storage** de forma padronizada.  

---

### 3.3 Bicep
- **O que é:** linguagem de alto nível (mais legível que JSON) para escrever IaC no Azure.  
- **Como funciona:** arquivo `.bicep` → compila para **JSON ARM** → o **ARM** executa.  
- **Vantagens:** sintaxe limpa, modular, fácil de manter; excelente suporte no VS Code/IntelliSense.  
- **Resumo:** o **ARM lê JSON**; o **Bicep facilita a escrita** desses templates.  

---

## 4. Azure Arc
- **O que é:** solução que **estende o ARM** para recursos fora do Azure (on-premises, outras nuvens e borda).  
- **Finalidade:** gerenciar/inspecionar servidores, VMs e clusters Kubernetes **externos** como se estivessem no Azure.  
- **O que permite:** aplicar **Azure Policy, RBAC, Tags, Defender for Cloud, Monitor/Logs** e práticas de **GitOps** (Kubernetes) em recursos não-Azure.  
- **Exemplo prático:** aplicar uma **Policy** que exige criptografia em **SQL Server on-premises** registrado no Arc.  
- **Resumo:** **Azure Arc = governança híbrida/multicloud** usando as mesmas ferramentas do Azure.  

---

## 5. Comparativo das Ferramentas

| Ferramenta        | Tipo             | Melhor uso                                   | Exemplo prático              |
|-------------------|------------------|----------------------------------------------|------------------------------|
| **Azure Portal**  | GUI              | Tarefas rápidas, aprendizado, troubleshooting | Criar VM manualmente         |
| **Cloud Shell**   | Terminal web     | CLI/PowerShell sem instalar nada              | Executar script no navegador |
| **PowerShell**    | Script (Az)      | Automação em Windows/Administração            | Script criar 10 VMs          |
| **CLI**           | Script (`az`)    | Automação multiplataforma/DevOps              | Pipeline criar RG e VM        |
| **ARM**           | Plano de controle| Governança e orquestração de recursos         | Aplica RBAC/Policy/Locks     |
| **ARM Templates** | IaC (JSON)       | Infraestrutura declarativa oficial            | Criar rede + storage + VMs   |
| **Bicep**         | IaC (linguagem)  | Escrever templates ARM de forma simples       | Template modular e legível   |
| **Azure Arc**     | Extensão         | Governança híbrida/multicloud                 | Policy em servidor on-prem   |

---

## 6. Resumo para a Prova AZ-900
- **Azure Portal:** GUI intuitiva para criar/gerenciar recursos.  
- **Azure Cloud Shell:** terminal no navegador com **CLI/PowerShell** prontos.  
- **Azure PowerShell:** automação em **PowerShell** (módulo Az), ideal para admins Windows.  
- **Azure CLI:** automação **multiplataforma** com saída **JSON**, ótima para DevOps.  
- **ARM:** plano de controle que aplica **RBAC/Policy/Locks** e orquestra providers.  
- **ARM Templates (JSON):** IaC declarativa oficial e idempotente do Azure.  
- **Bicep:** linguagem mais legível que gera o JSON consumido pelo ARM.  
- **Azure Arc:** estende a governança do Azure para ambientes **on-premises/multicloud**.  
