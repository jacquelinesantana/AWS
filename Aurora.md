# **Título da Aula: Explorando o AWS Aurora - O Banco de Dados na Nuvem**

------

## **Parte Teórica **

### **1. O que é o Amazon Aurora? **

- **Definição**:
  - Serviço de banco de dados relacional gerenciado na AWS.
  - Compatível com MySQL e PostgreSQL.
  - Combina desempenho e disponibilidade com custo-benefício.
- **Destaques**:
  - 5 vezes mais rápido que o MySQL comum e 3 vezes mais rápido que o PostgreSQL.
  - Auto-escalável e com alta disponibilidade.
- **Exemplo do Mundo Real**:
  - Aurora é usado para sites, sistemas de e-commerce, e até jogos online.

------

### **2. Benefícios do Amazon Aurora **

- **Escalabilidade Automática**: ajusta capacidade conforme a demanda.
- **Alta Disponibilidade**: replicações automáticas em múltiplas zonas de disponibilidade.
- **Gerenciamento Simples**: atualizações automáticas, backups contínuos.

------

### **3. Conceitos Básicos do Aurora **

- **Cluster de Bancos de Dados**: Conjunto de instâncias que compartilham o mesmo armazenamento.
- **Instância Primária**: Lida com gravações.
- **Instâncias Réplicas**: Lidam com leitura.

------

### **4. Como Criar e Usar o Aurora? **

- **Interface Simples**: Criar banco de dados no console AWS.
- **Prática Simples**: Vamos criar um banco Aurora e interagir com ele!

------

## **Parte Prática **

### **Passo 1: Criar o Banco de Dados**

1. **Acesse o Console AWS**:
    https://aws.amazon.com/console
2. **Abra o Amazon RDS**:
   - No menu, escolha "RDS".
3. **Crie um Cluster de Banco de Dados Aurora**:
   - Clique em "Create database".
   - Escolha "Amazon Aurora".
   - Selecione "MySQL" como mecanismo.
   - Opte por "Serverless" (para simplificar e economizar custos).
4. **Configuração Básica**:
   - Nome do banco: `school`.
   - Nome do usuário: `admin`.
   - Senha: `password123`.
   - Finalize clicando em "Create database".
   - Ajuste seu banco de dados para aceitar conexão externa em: Connectivity & security -> Publicly accessible


------

### **Passo 2: Conectar ao Banco de Dados**

1. Instale um cliente MySQL local (exemplo: MySQL Workbench ou DBeaver).
2. Pegue as informações de conexão (endpoint, porta, usuário, senha) no console RDS.
3. Conecte ao banco de dados usando o cliente.

------

### **Passo 3: Criar Tabela e Inserir Registro**

No cliente, execute os comandos SQL abaixo:

```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    age INT NOT NULL
);

INSERT INTO students (name, age) VALUES ('João', 16);

SELECT * FROM students;
```

------
## Comparando o RDS for Mysql com o Aurora for Mysql
1. Arquitetura e Armazenamento:

- RDS for MySQL:

Usa arquitetura tradicional MySQL;
Armazenamento EBS padrão;
Limite de 16TB por instância;
Backup e réplicas mais lentos por serem baseados em snapshots;

- Aurora MySQL:

Arquitetura distribuída proprietária da AWS;
Armazenamento distribuído em 6 cópias em 3 zonas de disponibilidade;
Limite de 128TB por cluster;
Backup e réplicas mais rápidos por serem contínuos e distribuídos;


2. Performance:

- RDS MySQL:

Performance similar ao MySQL on-premises;
Latência de escrita/leitura padrão MySQL;
Bom para cargas de trabalho até 2000-3000 transações por segundo;

- Aurora MySQL:

Até 5x mais performance que MySQL padrão;
Latência muito menor em escritas/leituras;
Pode lidar com 100.000+ transações por segundo;
Auto-scaling de leituras com até 15 réplicas;


3. Custos:

- RDS MySQL:

Cobra por hora da instância + armazenamento EBS;
Mais econômico para bancos pequenos/médios;
Bom custo-benefício até 1TB de dados;
Preço previsível e linear;

- Aurora MySQL:

Cobra por hora do cluster + IO + armazenamento;
Mais caro para bancos pequenos;
Melhor custo-benefício para grandes volumes;
Preço pode variar conforme uso;


4. Casos de Uso Ideais:

- RDS MySQL:

Aplicações pequenas e médias;
Startups e MVPs;
Cargas previsíveis;
Até 2000-3000 transações/segundo;
Dados até 1-2TB;
Orçamento limitado;
Quando não precisa de alta disponibilidade complexa;

- Aurora MySQL:

Aplicações enterprise;
E-commerces de alto tráfego;
Sistemas que precisam de escalabilidade rápida;
Mais de 3000 transações/segundo;
Dados acima de 2TB;
Necessidade de alta disponibilidade;
Sistemas críticos que não podem ter downtime;


I. Quando Justifica Usar Aurora:

- Número de Acessos:

A partir de 3000-5000 transações por segundo;
Mais de 10.000 queries por minuto;
Picos de acesso frequentes e imprevisíveis;
Aurora pode escalar até 200.000 queries por segundo;

- Outros Critérios:

Necessidade de disponibilidade 99.99%;
Replicação global;
Recovery time objective (RTO) muito baixo;
Backups sem impacto na performance;
Necessidade de scaling automático;
Budget não é a principal preocupação;


- Considerações para Escolha:

a. Escolha RDS MySQL se:

Está começando um projeto;
Tem orçamento limitado;
Carga de trabalho é previsível;
Não precisa de recursos avançados de HA;
Dados são menores que 1TB;
Até 2000 transações/segundo;

b. Escolha Aurora MySQL se:

Precisa de alta performance;
Tem orçamento mais flexível;
Carga de trabalho é variável;
Precisa de alta disponibilidade;
Dados maiores que 2TB;
Mais de 3000 transações/segundo;

- Aurora se paga quando:

O custo de downtime é alto;
Precisa de recuperação rápida;
Tem equipe capacitada para gerenciar;
Volume de dados justifica o investimento;
Necessita de replicação global;
Performance é crítica para o negócio;

## **Conclusão **

- **Resumo**: Aurora é fácil de usar, escalável e ótimo para sistemas modernos.
- **Dúvidas?**: Responda perguntas e estimule curiosidade.

Com essa abordagem, os adolescentes terão um entendimento prático e conceitual sobre o Amazon Aurora!

### **Perguntas e Respostas sobre AWS Aurora**

1. **O que é o Amazon Aurora e como ele é diferente de outros bancos de dados na AWS?**
   - O Aurora é um banco de dados relacional gerenciado, compatível com MySQL e PostgreSQL, projetado para oferecer alta performance, escalabilidade e disponibilidade. Ele é mais rápido que RDS MySQL/PostgreSQL e combina características empresariais com custo reduzido.
2. **Aurora suporta quais motores de banco de dados?**
   - Amazon Aurora suporta MySQL e PostgreSQL.
3. **Qual a diferença entre o Aurora Serverless e o Aurora provisionado?**
   - **Serverless** ajusta automaticamente a capacidade de acordo com a demanda, ideal para cargas variáveis.
   - **Provisionado** exige que o usuário configure manualmente o tamanho das instâncias.
4. **O que é um cluster no Amazon Aurora?**
   - Um cluster é um conjunto de instâncias que compartilham o mesmo armazenamento, incluindo uma instância primária (escrita) e réplicas de leitura.
5. **Como funciona a alta disponibilidade no Aurora?**
   - Os dados são automaticamente replicados em três zonas de disponibilidade (AZs) para tolerância a falhas.
6. **O Aurora faz backup automático? Como isso funciona?**
   - Sim, Aurora realiza backups contínuos no Amazon S3 e permite restaurar o banco em um ponto no tempo.
7. **Qual é o custo estimado para usar o Aurora em projetos pequenos?**
   - Depende do uso, mas o Aurora Serverless é ideal para projetos pequenos devido à cobrança baseada em tempo ativo.
8. **Quais são os casos de uso mais comuns do Aurora?**
   - Aplicativos web, e-commerce, sistemas de gestão, e soluções analíticas com alta demanda de leitura e escrita.
9. **Quais as principais vantagens de usar o Aurora em vez do MySQL padrão?**
   - Melhor performance (até 5x mais rápido), maior disponibilidade, backups automáticos e escalabilidade automática.
10. **Aurora suporta replicação em várias regiões?**
    - Sim, suporta replicação entre regiões (Global Database) para alta disponibilidade e baixa latência global.
11. **Posso migrar um banco de dados existente para o Aurora? Como?**
    - Sim, usando ferramentas como o AWS Database Migration Service (DMS) ou exportando/importando dados.
12. **Quais ferramentas podem ser usadas para conectar ao Aurora?**
    - MySQL Workbench, DBeaver, pgAdmin, ou qualquer cliente compatível com MySQL/PostgreSQL.
13. **É necessário gerenciar manualmente as atualizações no Aurora?**
    - Não, o Aurora suporta atualizações automáticas de software.
14. **Como funciona o escalonamento automático no Aurora Serverless?**
    - Ajusta a capacidade do banco de dados automaticamente com base na carga, sem intervenção manual.
15. **Aurora é seguro? Como configurar segurança para os dados armazenados?**
    - Sim, Aurora suporta criptografia em repouso e em trânsito, e permite configurar acesso com grupos de segurança e VPC.
16. **Como posso monitorar o desempenho do Aurora?**
    - Usando o Amazon CloudWatch, Performance Insights, ou métricas no Console AWS.
17. **O que é o endpoint de leitura e como ele funciona no Aurora?**
    - É um ponto de conexão que distribui as consultas de leitura entre réplicas no cluster, melhorando o desempenho.
18. **Como conectar o Aurora a uma aplicação web?**
    - Use o endpoint fornecido no console AWS, configurando-o no arquivo de configuração da aplicação.
19. **Aurora tem limites de armazenamento?**
    - O armazenamento cresce automaticamente até 128 TB.
20. **Posso usar o Aurora sem configurar VPC?**
    - Não, o Aurora exige que esteja associado a uma VPC para controle de rede e segurança.
21. **O que acontece se uma instância no cluster Aurora falhar?**
    - Uma réplica de leitura assume como instância primária automaticamente (failover).
22. **Como são cobrados os custos de armazenamento no Aurora?**
    - Com base na quantidade de dados armazenados e backups realizados.
23. **Qual é o impacto da latência de rede no desempenho do Aurora?**
    - Aurora otimiza latência usando replicação interna de alta performance entre as zonas de disponibilidade.
24. **Existe um modo de teste gratuito para o Aurora?**
    - Não há free tier dedicado, mas o Aurora Serverless permite baixo custo para testes de pequena escala.
25. **Qual é a diferença entre backup automático e snapshot manual no Aurora?**
    - Backup automático é contínuo, enquanto snapshots manuais são criados sob demanda e permanecem até serem excluídos.

## ##  Armazenamento no Amazon Aurora:

1. Os blocos de 10 GB:
   - O armazenamento do Amazon Aurora **autoescala em blocos de 10 GB** conforme necessário.
   - É uma **única unidade lógica de armazenamento compartilhada** por todas as instâncias do cluster (primária e réplicas de leitura).
   - Ou seja, **não há unidades separadas por instância**. Todas as instâncias do cluster acessam o mesmo volume de armazenamento subjacente.

------

### **Como os dados são gerenciados no armazenamento do Aurora:**

1. **Volume Distribuído:**
   - O volume de armazenamento do Aurora é distribuído em **três Zonas de Disponibilidade (AZs)**.
   - Cada AZ mantém **duas cópias dos dados** (total de seis cópias).
2. **Resiliência a falhas:**
   - Se um bloco de 10 GB sofrer falha (por exemplo, por falha de hardware ou indisponibilidade de uma AZ), o Aurora usa as cópias nas outras AZs para continuar operando.
   - O sistema detecta automaticamente a falha e substitui a cópia danificada sem intervenção manual.
3. **Alta Disponibilidade:**
   - Como todas as instâncias do cluster acessam o mesmo volume de armazenamento compartilhado, a perda de dados em uma unidade de armazenamento não afeta a operação do cluster.
   - O Aurora promove failover automático para réplicas de leitura, caso a instância primária seja afetada.

------

### **Resumo das Características:**

1. **Unidade única e compartilhada:**
    Todas as instâncias acessam o mesmo armazenamento subjacente, que é um volume lógico distribuído.
2. **Autoescala em blocos de 10 GB:**
    À medida que os dados crescem, novos blocos são alocados automaticamente até o limite de 128 TB.
3. **Alta Resiliência:**
   - Se uma cópia de dados falhar, há até cinco cópias restantes para garantir continuidade.
   - A replicação em três AZs proporciona tolerância a falhas de hardware e zonas inteiras.

------

### **Se os dados de uma unidade forem perdidos:**

- Não há impacto imediato, porque as **cópias restantes garantem continuidade**.
- O Aurora recria automaticamente a cópia perdida a partir das outras cópias disponíveis, sem necessidade de ação do administrador.

### **Por que isso importa como Arquiteto de Soluções?**

- Você pode projetar sistemas confiáveis com base no modelo de resiliência e redundância do Aurora, sem se preocupar com a perda de dados ou necessidade de provisionamento manual de armazenamento.
- O Aurora atende cargas críticas com **alta disponibilidade**, ideal para aplicações onde a perda de dados ou downtime seria inaceitável.

Prática: https://www.youtube.com/watch?v=SnCWucCEFLw

 ## Perguntas para estudar esse tema:

------

### **Perguntas e Respostas**

1. **O que é o Amazon Aurora?**
   - **Resposta:** É um serviço de banco de dados relacional gerenciado pela AWS, compatível com MySQL e PostgreSQL, projetado para oferecer alta disponibilidade, desempenho e escalabilidade.
2. **Quais mecanismos de banco de dados o Aurora suporta?**
   - **Resposta:** MySQL e PostgreSQL.
3. **Como o Amazon Aurora gerencia a alta disponibilidade?**
   - **Resposta:** Ele usa armazenamento distribuído, replicando dados automaticamente em três Zonas de Disponibilidade (AZs) para garantir resiliência e failover automático.
4. **O Aurora é um serviço serverless?**
   - **Resposta:** Sim, o Aurora oferece o **Aurora Serverless**, uma opção sem servidor que escala automaticamente a capacidade de banco de dados com base na demanda.
5. **Quais são as principais vantagens do Aurora em comparação com bancos de dados autogerenciados?**
   - **Resposta:** Gerenciamento automatizado, alta disponibilidade, desempenho otimizado, escalabilidade automática e backups contínuos para o Amazon S3.
6. **Qual o limite máximo de armazenamento do Amazon Aurora?**
   - **Resposta:** O Aurora pode escalar automaticamente até 128 TB por cluster.
7. **O que é um endpoint de leitura no Amazon Aurora?**
   - **Resposta:** Um endpoint usado para distribuir consultas de leitura entre as réplicas de leitura no cluster.
8. **Como o Aurora lida com falhas na instância primária?**
   - **Resposta:** Ele promove automaticamente uma réplica de leitura a instância primária para garantir continuidade.
9. **Quais tipos de backups o Aurora suporta?**
   - **Resposta:** Backups automáticos contínuos para o Amazon S3 e snapshots manuais.
10. **Quais casos de uso são ideais para o Aurora?**
    - **Resposta:** Aplicações de e-commerce, sistemas de gerenciamento financeiro e aplicativos empresariais críticos que exigem alta disponibilidade e escalabilidade.
11. **O Aurora oferece compatibilidade com o RDS Multi-AZ?**
    - **Resposta:** Sim, ele oferece suporte a arquitetura Multi-AZ com failover automático.
12. **O que é o Aurora Global Database?**
    - **Resposta:** É uma funcionalidade que permite a replicação de um banco de dados Aurora em várias regiões da AWS para melhor desempenho e recuperação de desastres.
13. **Como o Aurora Serverless escala?**
    - **Resposta:** Ele ajusta automaticamente a capacidade do banco de dados com base na demanda de uso.
14. **O Aurora suporta réplicas de leitura em diferentes regiões?**
    - **Resposta:** Sim, através do recurso **Aurora Global Database**.
15. **Qual o intervalo de tempo de recuperação de falha de uma instância Aurora?**
    - **Resposta:** Geralmente, a recuperação de falha é concluída em menos de 30 segundos.
16. **Você paga pelo armazenamento provisionado no Aurora?**
    - **Resposta:** Não, você paga pelo armazenamento usado e ele escala automaticamente.
17. **O Aurora é adequado para cargas de trabalho de baixa demanda?**
    - **Resposta:** Sim, especialmente com o Aurora Serverless, que reduz custos ao ajustar a capacidade automaticamente.
18. **O Amazon Aurora oferece suporte a replicação de leitura?**
    - **Resposta:** Sim, você pode configurar até 15 réplicas de leitura.
19. **Qual é a diferença entre Amazon Aurora e Amazon RDS?**
    - **Resposta:** O Aurora é otimizado para desempenho e alta disponibilidade com armazenamento distribuído e escalável, enquanto o RDS suporta mais mecanismos de banco de dados, mas sem as otimizações específicas do Aurora.
20. **O Aurora permite conexões de APIs personalizadas?**
    - **Resposta:** Sim, com Aurora MySQL você pode usar o recurso de **Aurora Custom Endpoints** para configurar endpoints personalizados.
21. **O Aurora oferece suporte a encriptação?**
    - **Resposta:** Sim, ele suporta encriptação em repouso e em trânsito usando o AWS Key Management Service (KMS).
22. **Como o Aurora Serverless ajuda a economizar custos?**
    - **Resposta:** Ele dimensiona automaticamente a capacidade do banco de dados para atender à demanda, evitando o provisionamento excessivo.
23. **O Aurora tem suporte para auditoria de logs?**
    - **Resposta:** Sim, ele suporta auditoria de logs usando o Amazon CloudWatch e outros serviços.
24. **É possível migrar para o Aurora de outro banco de dados?**
    - **Resposta:** Sim, usando o **AWS Database Migration Service (DMS)**.
25. **Quais ferramentas da AWS podem ser usadas com o Aurora?**
    - **Resposta:** Você pode usar o CloudWatch para monitoramento, o DMS para migração e o IAM para controle de acesso.

------



