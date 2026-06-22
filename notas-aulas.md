# 📝 Notas das Vídeo-aulas

Anotações organizadas por tema conforme assistidas durante a trilha. Use este arquivo como complemento ao `README.md` — aqui o foco é registrar pontos específicos, "pegadinhas" e explicações mais detalhadas de cada etapa.

---

## Aula 1 — Introdução ao Azure SQL

**Pontos principais:**
- O Azure SQL é uma "família" de produtos, não um produto único. Existem 3 modelos de implantação:
  1. SQL Server em VM (IaaS)
  2. SQL Managed Instance (PaaS com alta compatibilidade)
  3. SQL Database (PaaS)
- A escolha entre eles depende do nível de controle necessário vs. esforço de gerenciamento que se quer evitar.

**Anotação pessoal:**
> A "régua" mental que ajuda a decidir: quanto mais próximo de "quero migrar meu SQL Server tal como ele é hoje", mais perto de Managed Instance ou VM. Quanto mais próximo de "estou construindo algo novo, nativo de nuvem", mais perto de SQL Database.

---

## Aula 2 — Criando o Resource Group

**Pontos principais:**
- Resource Group = "pasta lógica" onde ficam agrupados todos os recursos relacionados a um projeto;
- Facilita gerenciamento de custos, permissões e exclusão em lote;
- Boa prática de nomenclatura: prefixo `rg-` + nome do projeto + ambiente (ex: `rg-sqlmi-lab-dev`).

---

## Aula 3 — Virtual Network (VNet) e sub-redes

**Pontos principais:**
- A Managed Instance **precisa** estar dentro de uma VNet — isso é uma característica que a diferencia do SQL Database;
- A sub-rede usada pela Managed Instance deve ser **dedicada** (sem outros recursos);
- A VNet pode ser criada antes ou durante o processo de criação da própria instância (o portal oferece a opção de criar tudo junto).

**Conceito que vale reforçar:**
- **VNet** = a "rede" maior, isolada de outras redes;
- **Sub-rede (subnet)** = uma subdivisão dentro da VNet, com seu próprio range de IPs.

---

## Aula 4 — Criando a Managed Instance no Portal

**Pontos principais:**
- O processo segue o padrão de "wizard" do Azure: Básico → Rede → Segurança → Compute/Storage → Tags → Revisão;
- Durante a etapa de autenticação, é definido o login `sqladmin` (ou nome customizado) e a senha;
- **Tempo de provisionamento real observado:** confirma a documentação oficial — o processo demorou um tempo considerável (várias horas) na primeira execução, por causa da preparação da infraestrutura de rede dedicada.

**Pegadinha identificada:**
> Em assinaturas gratuitas/estudante, é comum encontrar erro de cota de vCore insuficiente em determinadas regiões. Solução: tentar outra região ou reduzir o tier de compute solicitado.

---

## Aula 5 — Modelo de cobrança (vCore-based)

**Pontos principais:**
- Diferente do modelo DTU (usado em versões mais antigas do Azure SQL Database), a Managed Instance usa exclusivamente o modelo **vCore**;
- Custo = função de (vCores escolhidos) + (armazenamento provisionado) + (tier escolhido: General Purpose ou Business Critical);
- Existe a opção de **Reserved Capacity** (compra reservada) para quem sabe que vai manter o recurso por 1 ou 3 anos, com desconto significativo.

---

## Aula 6 — Conectando e validando a instância

**Pontos principais:**
- Ferramentas de conexão recomendadas: SSMS, Azure Data Studio, ou extensão `mssql` do VS Code;
- Por padrão, **não há endpoint público** — a conexão inicial precisa ser feita de dentro da mesma VNet (ex: via uma VM jump-box) ou habilitando explicitamente o acesso público com regras de firewall.
- A connection string fica disponível diretamente no portal, na blade do recurso.

---

## Aula 7 — Boas práticas e encerramento do lab

**Pontos principais:**
- Sempre **excluir os recursos** ao final de um lab de estudo para evitar cobranças;
- Documentar o processo (como este próprio repositório) ajuda a fixar o conteúdo e serve de referência futura;
- Vale revisar a documentação oficial sempre que for implementar em um cenário real, pois detalhes de UI/limites de cota mudam com frequência.

---

## ✅ Checklist de acompanhamento

- [x] Aula 1 — Introdução ao Azure SQL
- [x] Aula 2 — Resource Group
- [x] Aula 3 — VNet e sub-redes
- [x] Aula 4 — Criação da Managed Instance
- [x] Aula 5 — Modelo de cobrança
- [x] Aula 6 — Conexão e validação
- [x] Aula 7 — Boas práticas e cleanup
