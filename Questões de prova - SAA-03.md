# Questões de prova - SAA-03

Limitar acesso a serviços ou ações específicas em todas as contas AWS da equipe, as contas estão no AWS Organizations. A solução deve ser escalável e deve haver um único ponto onde as permissões possam ser mantidas.

<u>R: Crie uma política de controle de serviço na unidade organizacional rais para negar acesso aos serviços ou ações.</u>

Empresa produz dados de eventos e quer usar AWS para processar os dados à medida que são recebidos, os dados são escritos em uma ordem que deve ser mantida durante o processamento. A solução deve minimizar a sobrecarga operacional.

<u>R: Criar uma fila FIFO da Amazon SQS para manter as mensagens. Configurar a função AWS Lambda para processar as mensagens da fila.</u>

Empresa usa Aurora como repositório de dados para seu aplicativo de E-commerce global. Quando executa grandes relatórios os desenvolvedores relatam que o app esta tendo um desempenho ruim. Após revisar as métricas no Amazon CloudWatch, um arquiteto descobre que as métricas ReadIOPS e CPUUtilization estão disparando quando os relatórios mensais são executados. Solução mais econômica:

<u>R:Migrar os relatórios mensais para Amazon Redshift</u>

Empresa executa um app ServeLess publicamente acessível que usar o Amazom API Gateway e o AWS Lambda. Ocorrem atualmente solicitações fraudulentas de botnets. Quais etapas um arquiteto de soluções deve tomar para bloquear as solicitações de usuários não autorizados.

<u>R: Crie um plano de uso com uma chave de API que é compartilhada apenas com usuários genuínos</u>

<u>R: Implemente uma regra AWS WAF para direcionar solicitações maliciosas e acionar ações para filtrá-las</u>

Portal web que fornece aos usuários notícias globais de ultima hora, alertas e atualizações meteorológicas. O conteúdo é servido por HTTPS através de um servidor API executado em uma instância Amazon EC2 por trás de um ALB. A empresa quer que o portal forneça esse conteúdo aos seus usuários em todo mundo o mais rápido possível. Solução com menos latência para todos os usuários

<u>R: Implemente a pilha de aplicativos em uma única região AWS, use o Amazon CloudFront para servir todo conteúdo estático e dinâmico especificando o ALB como uma origem.</u>

Empresa usa o AWS Organizations para criar contas dedicadas da AWS para cada unidade de negócios para gerenciar a conta de cada unidade de negócios de forma independente mediante solicitação. O destinatário de e-mail raiz perdeu uma notificação que foi enviada para o endereço de e-mail do usuário raiz de uma conta. A empresa quer garantir que todas a notificações futuras não sejam perdidas. As notificações futuras devem ser limitadas aos administradores de conta. 

<u>R: Configure todos os endereços de e-mail do usuário raiz da conta AWS como lista de distribuição que vão para alguns administradores que podem responder aos alertas. Configure contatos alternativos da conta AWS no console AWS Organizations ou programaticamente.</u>

Empresa esta migrando app do on-premises para instâncias EC2. O arquiteto deve implementar alarmes de métrica de infraestrutura. Se a utilizalização da CPU aumentar para mais de 50% e os IOPS de leitura no disco estiverem altos ao mesmo tempo a empresa precisa agir o mais rápido possível, o arquiteto deve reduzir falsos alarmes.

<u>R: Criar alarmes compostos do Amazon CloudWatch sempre que possível.</u>

Empresa esta desenvolvendo um app de compartilhando de arquivos que usará uma bucket Amazon S3. Todos os arquivos são servidos via CloudFront, não deve ocorrer o acesso direto via URL do S3.

<u>R: Crie uma identidade de acesso de origem (OAI). Atribua a OAI a distribuição CloudFront. Configure as permissões de bucket S3 para que o OAI tenha permissão de leitura.</u>

Banco de dados Oracle local. Empresa deseja atualizar esse banco e configurar a recuperação de desastres DR para o banco. A empresa precisa minimizar a sobrecarga operacional para operações normais e configuração de DR. É necessário manter acesso ao sistema operacional subjacente.

<u>R: Migre o banco de dados Oracle para o Amazon RDS para Oracle. Crie uma réplica de leitura para o banco de dados em outra região AWS.</u>

Infraestrutura escalável de gerenciamento de chaves para suportar desenvolvedores que precisam criptografar dados em suas aplicações. Como reduzir a carga operacional?

<u>R: Use AWS Key Management Service (AWS KMS) para proteger as chaves de criptografia</u>

Empresa usa uma EC2 para todas as camadas de uma aplicação, esta apresentando degradação de desempenho nos horários de pico. Solução mais econômica:

<u>R: Migre o banco de dados para uma instância Amazon Aurora MYSQL. Crie uma AMI do aplicativo web. Aplique a AMI a um template de lançamento. Crie um grupo de auto Scaling com o template de lançamento. Configure o template de lançamento para usar uma Spot Fleet. Anexe um application Load Balancer ao grupo de auto Scaling.</u>

Equipe de relatórios recebe dados via S3 todos os dias e a equipe precisa migrar esses dados para um segundo S3 de analise e usar o Amazon Quicksight e também requer usar funções lambda para executar codigo, a equipe precisa enviar os dados para um Amazon Sagemaker Pipelines:

<u>R: Configure a replicação do S3 entre buckets. Configure o bucket de análise S3 para enviar notificações de eventos para o Amazon EventBridge. Configure uma regra ObjectCreated no EventBridge. Configure Lambda e SageMaker Pipelines como destino para a regra.</u>

Equipe de jogos e arquitetura altamente disponível, app executado em um Kernel Linux suporta tráfego em UDP e a empresa precisa de front end com melhor experiência possível com baixa latência.

<u>R: Configurar o AWS Global Accelerator para encaminhar solicitações para o Network Load Balancer. Usar instâncias EC2 para o aplicativo e um grupo de auto Scaling EC2.</u>

API distribuída pelo Cloudfront, contem informações confidenciais enviadas pelos usuários. O api usa HTTPS mas precisa de outra camada de segurança. as informações devem ser protegidas em toda pilha do aplicativo e o acesso as informações deve ser restrito a certos aplicativos.

<u>R: Configurar um perfil de criptografia de nível de campo do CloudFront.</u>

Dados em relatórios devem ser vistos globalmente como páginas HTML estáticas.

<u>R: Usar Amazon CloudFront com bucket S3 como sua origem.</u>

Aplicativo executado em uma frota de instâncias. Aplicativo lê dados de uma fila SQS e processa s mensagens em paralelo. O volume de mensagens é imprevisível e frequentemente tem tráfego intermitente. Atender de forma mais economica.

<u>R: Use instâncias reservadas para a capacidade básica e use instâncias Spot para lidar com a capacidade adicional.</u>

Site que atende evento terá vídeos das apresentações em tempo real e depois ficam disponíveis sob demanda. Público global como melhorar o desempenho do Streaming em tempo real.

<u>R: Amazon CloudFront.</u>

Aplicação possui autoScaling para uma única AZ e executa ALB como melhorar alta disponibilidade.

<u>R: Modifique o grupo de auto Scaling para usar três instâncias em cada uma das duas zonas de diponibilidade.</u>

Dados em lote que vem de diferentes bancos de dados e também dados de stream ao vivo de sensores de rede e APIs de aplicativos. É necessário consolidas todos os dados em um único lugar para análises. Os dados precisam ser processados e armazenados em diferentes buckets S3, as equipes executarão consultas únicas e importarão os dados para uma ferramenta de inteligência de negócios para mostrar indicadores chave de desempenho (KPIs). Qual a solução com menor sobrecarga operacional.

<u>R: Use o Amazon Athena para consultas únicas. Use o AMazon Quicksight para criar dashboards para KPIs</u>

<u>R: Use modelos na AWS Lake Formation para identificar os dados que podem ser ingeridos em um data lake. Use o AWS Glue para rastrear a fonte e extrair os dados e carregar os dados no Amazon S3 no formato Apache Parquet.</u>

Empresa quer baixar custo de sua instância de banco de dados RDS que opera apenas 12 horas por dia.

<u>R: Criar funções AWS Lambda para iniciar e parar a instância de banco de dados. Criar regras agendadas no Amazon EventBridge para invocar as funções Lambda. Configurar as funções Lambda como alvos de eventos para as regras.</u>

Uma empresa tem seus pedidos publicado como uma mensagem em uma fila RabbitMQ que é  executada em uma instância Amazon EC2 em uma única zona de  disponibilidade. Essas mensagens são processadas por um aplicativo  diferente que é executado em uma instância EC2 separada. Este aplicativo armazena os detalhes em um banco de dados PostgreSQL em outra instância EC2. Todas as instâncias EC2 estão na mesma zona de disponibilidade. A  empresa precisa redesenhar sua arquitetura para fornecer a maior  disponibilidade com a menor sobrecarga operacional. O que um arquiteto  de soluções deve fazer para atender a esses requisitos? 

<u>R: Migrar a fila para um par redundante(ativo/standby) de instâncias RabbitMQ no amazon MQ. Criar um grupo de Auto Scaling Multi-AZ para inatâncias EC2 que hospedam o aplicativo. Migrar o banco de dados para ser executado em uma implantação Multi-AZ do Amazon RDS for PostgreSQL</u>

E-commerce retorna erros de timeout devido auto demanda e processamento para banco de dados. Solução com o mínimo de alterações no aplicativo.

R: User o AWS WAF para proteger o Amazon API Gateway

Empresa tem um e-commerce onde cada pedido é executado em fila do RabbitMQ dentro de uma instância e os dados são enviados a um banco de dados PostgreSQL dentro de outra instância mesma AZ, como aumentar disponibilidade com menos sobrecarga operacional?

<u>R: Migrar a fila para um par redundante (Ativo/standby) de RabbitMQ no amazon MQ, criar um grupo de auto scaling multi AZ para inatâncias EC2 que hospedam o aplicativo. Migrar o banco de dados para ser executado em uma implantação Multi-AZ do Amazon RDS for PostgreSQL</u></u>

Empresa quer proteger a plataforma contra exploits web como injeção de SQL e também detectar e mitigar grandes ataques DDoS

<u>R: Use o AWS WAF para proteger o Amazon API Gateway</u>

<u>R: Use o AWS Shield Advanced com NLB</u>

Backup como solução de recuperação de desastres, os dados devem ser acessados em milessegundos se necessário e o armazenamento será por 30 dias.

<u>R: S3 Standard</u>

Migrar banco de dados do on-premises para o Aurora PostgreeSQL sem tirar o on-premises do ar durante a migração.

<u>R: Criar uma tarefa de replicação continua.</u>

<u>R: Criar um servidor de replicação do AWS Database Migration Service (AWS DMS)</u>

Migrar dados do S3 (criptografados) para uma nova região e usar menor sobrecarga operacional. esses dados deve atender uma solução Serveless.

<u>R: Criar um novo bucket S3. Carregar os dados no novo Bucket. Usar a replicação entre regiões do S3(CRR) para replicar objetos criptografados para um bucket S3 em outra região. Use criptografia do lado do servidor com chaves multi-região do AWS KMS(SSE-KMS). Usar o Athena para consultar os dados.</u>

Empresa de mídia requer 10TB armazenamento com desempenho máximo de i/o para processamento de vídeo, 300TB para armazenamento durável e 900TB para atender arquivamento de mídia.

<u>R: Amazon EC2 instancia Store para desempenho máximo, Amazon D3 para armazenamento de dados duráveis e S3 Glacier para armazenamento arquivístico.</u> 

Aplicativo esta em Ec2 com Aplication Load Balancer, apresenta maior acesso no horário comercial, baixo acesso pós horário comercial e baixa procura aos finais de semana, como customizar custos de EC2?

<u>R: Use instâncias reservadas para nível básico de uso, usar instâncias Spot para qualquer capacidade adicional que o aplicativo precisar.</u>

Empresa usa Amazon DynamoDB para metadados de mídia. APP esta intensivo em leituras e apresenta atrasos. 

<u>R: Use o Amazon DynamoDB Accelerator(DAX).</u>

Empresa vende toques de celular que tem baixa procura após 90 dias.

<u>R: Implementar uma política de ciclo de vida do S3 que mova os objetos do S3 Standard para o S3 Standard Infrequent Access(S3 Standard 1A) após 90 dias.</u>

O arquiteto de soluções deve projetar solução que uso o CloudFront e uma origem S3 para site estático. Todo o trafego do site deve ser inspecionado pelo AWS WAF.

<u>R: Configure o CloudFront e o S3 para usar uma identidade de acesso de origem (OAI) para restringir o acesso ao bucket S3. Habilite o AWS WAF na distribuição.</u>

Site deve fornecer aos usuários relatórios de desempenho históricos para download, site é global e deve ter uma solução econômica.

<u>R: Amazon CloudFront e Amazon S3</u>

Otimizar custos de execução de um aplicativo na AWS, o App esta em EC2, Fargate e Lambda. O banco de dados esta na EC2, hospedar de forma econômica.

<u>R: Use Spot Instances para a camada de ingestão de dados.</u> 

<u>R: Comprar um compute Savings plan de 1 ano para a camada de Front-end e API</u>

Aplicativo web multicamada local em container. Melhorar a infra e migrar para AWS  com vários hosts Linux conectados a um banco de dados PostgreSQL.

<u>R: Migrar o aplicativo web para ser hospedado no AWS Fargate com o Amazon Elastic Container Service ECS</u>

<u>R: Migre o banco de dados PostgreSQL para o Amazon Aurora.</u>

Empresa coleta dados médicos em um S3, apenas um grupo de usuários pode inserir novos dados e os demais devem apenas acessar a leitura. Deve-se manter os arquivos por 1 ano.

<u>R: Use S3 Object Lock no modo de conformidade com um período de retenção de 365 dias.</u>

E-commerce em 2 camadas. Balanceador de cargas para a camada web em EC2, banco de dados usa uma instância para RDS. Estas instâncias não devem ser expostas para internet. Porem a camada web requer sair para internet para pagamento. Aplicação deve altamente disponível.

<u>R: Configure uma VPC com duas sub-redes públicas, duas sub-redes privadas e dois gateways NAT em duas zonas de disponibilidade. Implantar um ALB nas sub-redes públicas.</u>

<u>R: Usar um grupo de auto Scaling para lançar as instâncias EC2 em sub-redes privadas. Implantar a instância RDS Multi AZ em sub-redes privadas.</u>

Aplicação em EC2 várias AZs com Grupo de Auto Scaling e EC2 atrás de ALB, Melhor desempenho da instância esta no uso de CPU a 40%. 

<u>R: Use uma política de rastreamento de alvo para escalar dinamicamente o grupo de Auto Scaling.</u>

Aplicativo monolítico, migrar para AWS mantendo o máximo dos códigos back end e front-end.

<u>R: Hospedar o aplicativo no Amazon Elastic Container Service(ECS) Configurar um ALB com o ECS como alvo.</u>

Carga de trabalho de processamento de transações online (OLTP) na AWS, usa instância de banco de dados RDS não criptografada e uma multi-AZ. Snapshots diários do bando são feitos a partir dessa instância. Aplicar criptografia nos banco de dados e snapshots.

<u>R: Criptografar uma cópia do snapshot mais recente do banco de dados. Substituir a instancia do banco de dados existente restaurando o snapshot criptografado.</u>

Empresa com app web dinâmico hospedado em EC2 possui SSL e esta com aumento no tráfego. A ação de criptografia e descriptografia esta causando sobrecarga a capacidade computacional.

<u>R: Importar o certificado SSL no AWS Certificate Manager ACM. Criar um ALB com um listener HTTPS que usa o certificado SSL do ACM.</u>

Api que automatiza cálculos de impostos com base em preços de itens e tem grande número de consultas durante as férias, isso causa respostas mais lentas. Tornar essa aplicação escalável e elástica.

<u>R: Projetar uma API REST usando o Amazon API Gateway que aceite os nomes dos itens. O API Gateway passa os nomes do itens para o AWS Lambda para cálculos de impostos.</u>

2 Aplicações sendo a primeira de envio de mensagens de carga úteis a serem processadas e a segunda de processamento destinada a receber mensagens com carga úteis. Recebe e processa cerca de 1000 mensagens por hora e deseja terceirizar a troca de mensagens entre as duas pela AWS. Cada mensagem pode levar 2 dias para ser processada. A mensagem não pode deixar de ser processada. 

<u>R: Integrar as aplicações de envio e processamento com uma fila SQS. Configurar uma fila de mensagens não processadas(dead-letter queue) para coletar as mensagens que falharam no processamento.</u>

Cluster de Amazon Aurora PostgreSQL deve armazenar os dados por 5 anos e excluir todos os dados após 5 anos. os logs de auditoria e ações dentro do banco de dados também devem ser mantidos. Atualmente realiza backups automatizados. 

<u>R: Use o AWS Backup para fazer os backups e mante-los por 5 anos.</u>

<u>R: configure uma exportação do Amazon CloudWatch Logs para o cluster de banco de dados</u>

Cargas de trabalho na AWS e precisa se conectar a um serviço de um provedor externo. A equipe define que a conexão deve ser privada e restrita ao serviço de destino. A conexão deve ser iniciada apenas a partir da VPC da empresa.

<u>R: Peça ao provedor para criar um endpoint de VPC para o serviço de destino. Usar o AWS PrivateLink para se conectar ao serviço de destino.</u>

Armazenamento de logs, acesso regular no último mês, acesso raro para arquivos com mais de 1 mês. estimativa de 10TB de logs por mês. Forma de armazenamento mais econômica.

<u>R: Implantar uma distribuição web do Amazon CloudFront na frente do S3.</u>

Empresa de jogos, usuários consomem grande números de vídeos e imagens que são armazenados em S3. Este conteúdo é o mesmo para todos os usuários. App esta com milhões de usuários ao redor do mundo acessando esses arquivos de mídia. Reduzir os valores da solução enquanto fornece os arquivos aos usuários.

<u>R: Implante uma distribuição web do Amazon CloudFront na frente do S3.</u>

Reduzir custos de armazenamento de uma empresa. Todos os dados da empresa estão na classe de armazenamento S3 Standart. Os dados devem se manter armazenados por 25anos, e dados de até 2 anos devem estar altamente disponíveis.

<u>R: Configurar uma política de ciclo de vida S3 para transferir objetos para o S3 Glacier Deep Archive após 2 anos.</u>

Evitar ataques DDoS

<u>R: Habilitar o AWS Sield Advanced para prevenir ataques.</u>

Processamento em lote altamente dinâmico que usar muitas instâncias EC2. O trabalho é sem estado e pode ser iniciado e interrompido a qualquer momento sem impacto negativo e normalmente leva mais de 60 minutos para se concluído. Requer uma solução escalável e econômica que atenda aos requisitos.

<u>R: EC2 Spot</u>

Empresa oferece acesso a arquivos de mídia em cache para usuários ao redor do mundo, conteúdo esta em S3 e a empresa deve entregar o conteúdo rapidamente.

<u>R: Implantar o Amazon CloudFront para conectar os buckets S3 aos servidores de borda do CloudFront.</u>

Aplicativo Python que processa dados em Json e gera resultados em banco de dados SQL on-premises. O aplicativo é executado milhares de vezes a cada dia. Deve-se migra para AWS de forma altamente disponível que maximize a escalabilidade e minimize a sobrecarga operacional.

<u>R: Colocar os documentos Json em um bucket. Criar uma função Lambda que execute o código Python para processar os documentos à medida que chegam no S3. Armazenar os resultados em um cluster Amazon AuroraDB.</u>

EC2 em sub-redes privadas, precisa acessar o DynamoDB, qual a forma mais segura?

<u>R: Use endpoint VPC para o DynamoDB.</u>

Instancias EC2 e uma instância do RDS em uma única AZ. Fazer backup em uma região separada sem sobrecarga operacional.

<u>R: User o AWS Backup para copiar backups do EC2 e backups do RDS para a região destino.</u>

Infraestrutura de computação de alto desempenho na AWS para modelagem de risco financeiro. As cargas de trabalho da empresa rodam em Linux. Cada instância de trabalho é uma Spot (rodam centenas), tem curta duração e gera milhares de arquivos de saída que são armazenados em armazenamento persistente para análise e uso futuro a longo prazo. Copiar dados on-premises para nuvem de forma a ser persistente de longo prazo para tornar os dados disponíveis para processamento para as instâncias. 

<u>R: Amazon FSx for Lustre integrado com S3.</u>

Armazenar usuário e senha de um bando de dados que um aplicativo usa para acessar uma instância RDS a partir de outra instância. Deve-se criar um parâmetro seguro no AWS System Manager Parameter Store. 

<u>R: Criar uma função IAM que tenha acesso de leitura ao parâmetro do Parameter Store. Permita acesso de decriptação a uma chave AWS KMS que é usada para criptografia do parâmetro. Atribuir essa função IAM a instancia EC2.</u> 

Aplicativo Web deve ser executado em EC2 com ALB e recentemente a sua política foi alterado e exige que o app seja acessado apenas de um pais específico.

<u>R: Configurar o AWS WAF no ALB em uma VPC</u>

Migrar do on-premises para AWS e pode usar apenas uma região e AZ, e sem acesso a internet.

<u>R: Usar o AWS Organizations para configurar políticas de controle de serviço(SCPS) que impedem VPCs de obter acesso à internet. Negar acesso a todas as regiões AWS exceto a permitida.</u>

<u>R: Usar AWS Control Tower para implementar guardrails de residência de dados para negar acesso à internet e negar acesso a todas as regiões AWS, exceto a permitida.</u>

Containers na AWS, aplicações que podem toletar interrupções. 

<u>R: Usar Spot em um grupo de nós gerenciados do EKS.</u>

Implementar App do on-premises para a AWS o mesmo esta em container e deve atender alta demanda logo após ser implementado. Deve-se ter escala ser altamente disponível e minimizar a sobrecarga operacional.

<u>R: Armazenar imagens de contêiner em um repositório Amazon Elastic Container Registry(ECR). Usar um cluster Amazon Elastic Container Service com o tipo de lançamento AWS Fargate para executar os contêineres. Usar o rastreamento de alvo para escalar automaticamente com base na demanda.</u>

