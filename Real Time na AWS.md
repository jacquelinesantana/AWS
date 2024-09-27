# Real Time na AWS

O que é Streaming de dados:

- São dados processados em continuidade
- Requer baixa latência, processamento em tempo real (latência de milissegundos)
- Atender as necessidades do cliente enquanto o cliente esta no seu site
- Detectar fraudes de maneira mais ágil possível
- Ambientes não é possível obter lotes, faz-se necessário ir processando os dados a medida em que eles aparecem
- Monitorar redes sociais
- Monitorar infraestrutura
- Sistemas de recomendação
- Jogos online 
- Transmissão ao vivo
- Análise de clickstream
- Monitoramento de saúde em tempo real
- Processamento de transações em bolsa de valores

## Conceitos

### Streaming x Batch x Micro batches

- Streaming processa conforme a produção
- Batch processa em lote, dentro de um período de tempo
- Micro Batch - processamento em lote em intervalo bem curto (minuto a minuto) próximo do tempo real

### Produtores

Entidades que geram e enviam dados para o sistema de Streaming, podem ser sensores de IoT, Aplicações Web, Apis...

### Consumidores

Aplicações que recebem e/ou processam esse dados, podem ser dashboards em tempo real e sistemas de alerta

### Brokers

É um sistema intermediário que recebe os dados dos produtores e os distribui para os consumidores, exemplo um Apache Kafka, Kinesis e RabbitMQ.

Um serviço Broker trás para a aplicação:

- Disponibilidade e escalabilidade

- Durabilidade e persistência

- Baixa latência e processamento em tempo real

- Gestão de fluxo de dados complexos

- Garantia de entrega e ordem

- Monitoramento e gerenciamento

- Suporta fluxos complexos

  

### Outros:

- Topic: assunto
- Mensagem: dados
- Assinatura: um consumidor assina um topic

### Janelas

Processamento de um dado feito em partes menores, fragmento.

Tipos de janelas:

- Janela baseada em tempo(de x em x minutos...)
- Janela baseada em contagem: quantidade de mensagens recebidas
- Janelas deslizantes: exemplo calculo média móvel de temperatura a cada 15min
- Janela de Tumbling: segmenta os dados de maneira continuas e não sobrepostas - números de transações de um banco

### Garantia de entrega:

- At-most-once: pode haver perda, não pode haver duplicação dos dados
- At-least-once: não pode haver perda, pode haver duplicação dos dados
- Exactly-once: não pode haver perda, não pode haver duplicação dos dados

### Estratégias de escalabilidade:

1. Partitioning: divide os dados em partições menores e permite o processamento paralelo
2. Sharding: similar ao anterior divide os dados entre vários servidores/nós
3. Replicação: mantem copias dos dados para ter tolerância a falha
4. Auto Scaling: ajusta automaticamente os recursos com base na carga de trabalho(tamanho da fila)

### Estratégias a falhas:

1. Replicação de dados: múltiplas copias dos dados em diferentes nós
2. Checkpointing: salva periodicamente os dados
3. Failover Automático: redireciona automaticamente o processamento 
4. Processamento idempotente: garante que as operações repetidas resultem o mesmo resultado final e evita duplicar dados.

### Técnicas para baixar a latência:

- Parallel processing - processamento paralelo 
- In-Memory processing - processa tudo em memoria o que torna tudo mais rápido
- Optimização de rede - técnicas para otimizar a rede

## Projeto

Cenário: Sistema piloto de emissão de alertas climáticos em tempo real, com banco de dados para futuramente ter dashboards interativos e modelos estatísticos. Vamos abordar possibilidade de chuva, ventos... e os dados devem ser enviados por e-mail ou SMS.

### Api para consumo dos dados

tomorrow.io

- Oferece dados climáticos que podem ser atualizadas de hora em hora ou  diária com janela de 5 dias.
- Informações em tempo real Minuto a minuto
- Dados históricos
- Oferece até 500 requisições por dia grátis
- 25 requisições por hora
- 3 requisições por segundo

#### Para o projeto

- 1 requisição a cada 3 min, 480 chamadas por dia 24x7
- Criar conta gratuita no app.tomorrow.io
- Criar chave de API

### Serviços AWS

#### Lambda

Serviço de computação serveless que permite executar umcódigo em resposta de eventos, aceita diversas linguagens, vai fazer papel de consumer

#### IAM Role

Conjunto de permissões que precisamos atribuir as entidades

#### CloudWatch

Monitora recursos, vamos utilizar o seu evento para consultar a api e recuperar as informações climáticas

#### Kinesis

É o nosso sistema broker, plataforma para processar grandes fluxos de dados em tempo real. **Kinesis Data Streams** para coletar e processar dados em tempo real. **Kinesis Data Firehose** para carregar os Streams de dados em destinos como S3 e Redshift e **Kinesis Data Analytics** para análise de Streams de dados em tempo real.

#### S3 

Vai ser utilizado para armazenar os dados na medida e formato que ele chega.

#### Glue

Ferramenta de ETL(extração, transformação e carga) totalmente gerenciado que facilita a preparação e o carregamento de dados para análise. **Glue Crawler** automaticamente varre os dados em suas fontes, detectando o esquema e armazenando definições de tabela. **Glue Data Catolog**, atua como um repositório central de metadados.

#### SNS

Serviço de notificação para ajudar a ver anomalias com os dados.

#### Athena

Permite analisar dados diretamente no S3 usando SQL padrão.