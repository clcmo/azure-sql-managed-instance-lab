# 🗄️ Azure SQL Managed Instance Lab

Repositório criado como entregável do desafio de projeto **"Configurando um Banco de Dados na Azure"** da [Digital Innovation One (DIO)](https://www.dio.me/). Aqui documento o processo de criação de uma **Instância Gerenciada de SQL do Azure (Azure SQL Managed Instance)**, com resumos das aulas, anotações técnicas e dicas práticas para quem for replicar o laboratório.

---

## 📌 Sobre o desafio

O objetivo do desafio foi:

- Aplicar na prática os conceitos de configuração de banco de dados na Microsoft Azure;
- Documentar o processo técnico de forma clara e estruturada;
- Usar o GitHub como ferramenta de compartilhamento de conhecimento técnico.

---

## 🎯 O que é uma Azure SQL Managed Instance?

A **Azure SQL Managed Instance** é uma opção de implantação do Azure SQL que oferece compatibilidade quase total com o SQL Server local (on-premises), mas com a infraestrutura totalmente gerenciada pela Microsoft (patching, backups, alta disponibilidade, etc).

Ela fica posicionada "no meio do caminho" entre duas outras opções da família Azure SQL:

| Opção | Nível de gerenciamento | Compatibilidade com SQL Server | Caso de uso típico |
|---|---|---|---|
| **SQL Server em VM (IaaS)** | Você gerencia o SO e o SQL Server | 100% | Migração 1:1, controle total do ambiente |
| **Azure SQL Managed Instance** | Microsoft gerencia a infraestrutura | Muito alta | Migração "lift-and-shift" com mínimas alterações de código |
| **Azure SQL Database (PaaS)** | Microsoft gerencia tudo | Parcial | Aplicações novas, nascidas na nuvem |

### Principais vantagens
- 🔄 **Migração facilitada**: pensada para bancos on-premises migrarem para a nuvem com o mínimo de refatoração possível;
- 🔒 **Isolamento de rede**: vive dentro de uma **Virtual Network (VNet)**, o que aumenta a segurança;
- 🛠️ **Recursos avançados de SQL Server**: suporta SQL Agent, CLR, Service Broker, DB Mail, entre outros recursos que o Azure SQL Database (PaaS puro) não oferece;
- 📈 **Backups automáticos e Alta Disponibilidade** nativos, sem necessidade de configuração manual;
- 💰 **Modelo de cobrança flexível**: vCore-based, com opções de compra reservada para economia.

---

## 🧱 Pré-requisitos do laboratório

Antes de iniciar a criação da instância, é necessário ter:

- [ ] Uma conta ativa no [Azure Portal](https://portal.azure.com) (a conta gratuita/estudante é suficiente para o lab);
- [ ] Uma **Virtual Network (VNet)** e **sub-rede** já configuradas (ou permitir que o próprio assistente de criação gere uma);
- [ ] Permissões de **Contributor** (ou superior) na subscription/resource group utilizado;
- [ ] Entendimento básico de **grupos de recursos (Resource Groups)** no Azure.

> 💡 **Dica:** Se você está usando uma assinatura gratuita ou de estudante, fique atento aos limites de cota de vCore — a criação da Managed Instance pode falhar silenciosamente se a subscription não tiver cota disponível na região escolhida.

---

## 🚀 Passo a passo: criando a instância

Segui como referência principal o guia oficial da Microsoft: [Início Rápido: criar Instância Gerenciada de SQL do Azure](https://learn.microsoft.com/pt-br/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&tabs=azure-portal).

### 1. Acessar o Azure Portal
Login em [portal.azure.com](https://portal.azure.com) → buscar por **"Azure SQL"** na barra de pesquisa superior.

![Busca por Azure SQL no portal](images/01-busca-azure-sql.png)

### 2. Criar um novo recurso SQL
- Clique em **"+ Create"**;
- Selecione **SQL Managed Instances** → **Single Instance**.

![Tela de seleção de tipo de recurso SQL](images/02-selecao-tipo-recurso.png)

### 3. Configurar o básico (aba "Basics")
- **Subscription**: selecionar a assinatura ativa;
- **Resource Group**: criar um novo ou usar um existente (boa prática: nomear algo como `rg-sql-mi-lab`);
- **Managed Instance name**: nome único da instância (ex: `sqlmi-dio-lab`);
- **Region**: escolher uma região com cota disponível (ex: `Brazil South` ou `East US`, dependendo da disponibilidade);
- **Authentication**: definir o **usuário administrador** e a **senha** (anote em local seguro!).

![Aba Basics de configuração](images/03-aba-basics.png)

> ⚠️ **Atenção:** A senha do administrador precisa atender aos requisitos de complexidade do Azure (mínimo de caracteres, maiúsculas, minúsculas, números e símbolos).

### 4. Configurar rede (aba "Networking")
- Selecionar (ou criar) a **Virtual Network** e a **sub-rede** dedicada à Managed Instance;
- A sub-rede **não pode ser compartilhada** com outros recursos — é uma exigência do serviço.

![Configuração de rede](images/04-configuracao-rede.png)

### 5. Definir o tier de computação (aba "Compute + Storage")
- Escolher entre **General Purpose** (mais econômico, ideal para o lab) ou **Business Critical** (maior performance/HA);
- Ajustar vCores e armazenamento de acordo com a necessidade (para o lab, o mínimo já é suficiente).

![Configuração de compute e storage](images/05-compute-storage.png)

### 6. Revisar e criar
- Revisar todas as configurações na aba **"Review + create"**;
- Clicar em **"Create"** e aguardar a validação.

![Tela de revisão final antes da criação](images/06-revisao-final.png)

> ⏱️ **Dica importante:** A criação de uma SQL Managed Instance **não é instantânea** — pode levar de **algumas horas** (geralmente entre 4 e 6h na primeira implantação dentro de uma sub-rede nova). Isso é esperado e está documentado oficialmente pela Microsoft. Planeje o lab com isso em mente — não é erro de configuração se a barra de progresso demorar.

### 7. Conectar à instância
Após a implantação ser concluída, é possível conectar via:
- **SQL Server Management Studio (SSMS)**
- **Azure Data Studio**
- **mssql extension no VS Code**

Usando o **endpoint privado** gerado dentro da VNet (lembrando que, por padrão, a Managed Instance **não tem endpoint público habilitado** — é necessário configurar isso explicitamente se for preciso acessar de fora da rede).

![Tela de conexão via Azure Data Studio](images/07-conexao-instancia.png)

---

## 🧠 Conceitos-chave revisados nas aulas

- **IaaS vs PaaS vs SaaS**: entender onde a Managed Instance se posiciona (PaaS com características de IaaS);
- **Virtual Network (VNet) e sub-redes**: isolamento de rede como camada de segurança;
- **Resource Groups**: organização lógica de recursos relacionados no Azure;
- **vCore-based purchasing model**: modelo de cobrança baseado em núcleos virtuais + armazenamento, em vez de DTUs;
- **Backup automático e Point-in-Time Restore**: recursos nativos de recuperação de dados;
- **Failover Groups / Alta Disponibilidade**: réplicas automáticas para garantir disponibilidade.

---

## 💡 Dicas e observações práticas

1. **Cuidado com o tempo de provisionamento.** A primeira instância criada em uma sub-rede nova demora bastante (horas). Instâncias subsequentes na mesma sub-rede são mais rápidas.
2. **Cuidado com custos.** Mesmo em contas de estudante/gratuitas, a Managed Instance pode consumir créditos rapidamente — **delete o recurso ao final do lab** se não for usá-lo, para evitar cobranças inesperadas.
3. **Anote a connection string** logo após a criação — ela fica disponível na seção "Connection strings" do recurso no portal.
4. **A sub-rede é exclusiva.** Diferente de outros recursos do Azure, a Managed Instance exige uma sub-rede dedicada, sem outros recursos nela.
5. **Sem acesso público por padrão.** Se for testar fora da VNet (por exemplo, da sua máquina local), será necessário configurar um endpoint público e regras de firewall — ou usar uma VM jump-box dentro da mesma VNet.

---

## 🧹 Encerrando o lab (cleanup)

Para evitar custos desnecessários após o estudo:

```bash
# Via Azure CLI
az sql mi delete --name <nome-da-instancia> --resource-group <nome-do-resource-group>

# Ou, para remover todo o grupo de recursos criado no lab:
az group delete --name <nome-do-resource-group> --yes --no-wait
```

---

## 📚 Referências e recursos utilizados

- [Início Rápido: criar Instância Gerenciada de SQL do Azure (Microsoft Learn)](https://learn.microsoft.com/pt-br/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&tabs=azure-portal)
- [GitHub Quick Start - DIO](https://github.com/digitalinnovationone/github-quickstart)
- [GitBook: Formação GitHub Certification](https://aline-antunes.gitbook.io/formacao-fundamentos-github)
- [Documentação oficial do GitHub](https://docs.github.com/)
- [Guia de Markdown do GitHub](https://docs.github.com/pt/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

## 🗂️ Estrutura deste repositório

```
azure-sql-managed-instance-lab/
├── README.md          # Este arquivo - documentação principal
├── notas-aulas.md      # Anotações detalhadas por vídeo-aula
├── glossario.md        # Glossário de termos técnicos do Azure
└── images/              # Capturas de tela do processo
    ├── 01-busca-azure-sql.png
    ├── 02-selecao-tipo-recurso.png
    ├── 03-aba-basics.png
    ├── 04-configuracao-rede.png
    ├── 05-compute-storage.png
    ├── 06-revisao-final.png
    └── 07-conexao-instancia.png
```

---

## 👤 Autora

**Milla** — desenvolvedora e estudante de pós-graduação em Monitoramento Atmosférico.
🔗 [camilaloliveira.com](https://camilaloliveira.com) · ✉️ ola@camilaloliveira.com · 💻 GitHub: [@clcmo](https://github.com/clcmo)

---

> 📝 Repositório criado como parte do bootcamp/trilha da [Digital Innovation One (DIO)](https://www.dio.me/), com fins exclusivamente educacionais.
