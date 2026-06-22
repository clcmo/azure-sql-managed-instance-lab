# 📖 Glossário — Termos do Azure SQL

Pequeno dicionário de referência rápida com os termos mais usados ao longo do lab.

| Termo | Definição |
|---|---|
| **Azure SQL** | Família de produtos de banco de dados relacional totalmente gerenciados pela Microsoft, baseados no motor do SQL Server. |
| **SQL Managed Instance** | Modelo de implantação do Azure SQL com alta compatibilidade com SQL Server on-premises, infraestrutura gerenciada pela Microsoft. |
| **Resource Group (Grupo de Recursos)** | Contêiner lógico que agrupa recursos relacionados de um projeto/solução no Azure. |
| **Virtual Network (VNet)** | Rede virtual isolada dentro do Azure, usada para isolar e proteger recursos. |
| **Sub-rede (Subnet)** | Subdivisão de uma VNet com seu próprio intervalo de IPs; a Managed Instance exige uma sub-rede dedicada. |
| **vCore (Virtual Core)** | Unidade de medida de capacidade de processamento usada no modelo de cobrança vCore-based. |
| **DTU (Database Transaction Unit)** | Modelo de cobrança mais antigo, baseado em uma métrica combinada de CPU, memória e I/O (não usado pela Managed Instance). |
| **General Purpose** | Tier de serviço voltado a cargas de trabalho padrão, com bom custo-benefício. |
| **Business Critical** | Tier de serviço voltado a cargas de trabalho críticas, com maior performance e réplicas locais de alta disponibilidade. |
| **Failover Group** | Mecanismo de alta disponibilidade que permite failover automático entre regiões. |
| **Point-in-Time Restore (PITR)** | Recurso de backup que permite restaurar o banco para um momento específico no passado. |
| **Endpoint público** | Ponto de acesso à instância acessível pela internet (desabilitado por padrão na Managed Instance). |
| **Endpoint privado** | Ponto de acesso à instância acessível apenas dentro da VNet/rede configurada. |
| **SSMS (SQL Server Management Studio)** | Ferramenta gráfica da Microsoft para administração de instâncias SQL Server/Azure SQL. |
| **Azure Data Studio** | Ferramenta multiplataforma e mais leve que o SSMS, também usada para administrar bancos Azure SQL. |
| **IaaS (Infrastructure as a Service)** | Modelo de nuvem em que o provedor entrega a infraestrutura (VMs, redes, storage) e o cliente gerencia o SO e aplicações. |
| **PaaS (Platform as a Service)** | Modelo de nuvine em que o provedor gerencia a infraestrutura e a plataforma, deixando o cliente focado apenas na aplicação/dados. |
| **Reserved Capacity** | Modelo de compra antecipada (1 ou 3 anos) que oferece desconto em troca de compromisso de uso. |
