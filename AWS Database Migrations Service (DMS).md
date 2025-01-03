# AWS Database Migrations Service (DMS)

Serviço que facilita a migração de dados entre banco de dados de outras fontes (outros serviços ou onpremises) para a AWS RDS. Podemos então utilizar esse serviço para fazer migração de dados homogêneas ou heterogêneas. Ou seja, podemos migrar de um banco de dados Mysql para outro banco ainda dentro da plataforma Mysql ou de um Mysql para um Postgre ou outra plataforma.

Podemos também utilizar esse serviço para migrar dados de um banco de dados na AWS para um banco de dados onpremises, e isso tudo ser feito a manter o serviço operando e ter o mínimo possível de inatividade do sistema. 

O DMS não é compativel apenas com o RDS podemos utiliza-lo para migrar dados para o S3 e ou o Redshift(warehouse) 

É possível ainda migrar entre uma estrutura SQL para uma estrutura NOSQL com auxilio do DMS.

## Migração de dados homogênea

Etapas para a migração homogênea:

1. instância de replicação onde serão executadas as ações operações
2. definir a origem dos dados
3. definir o destino
4. migrar os dados da origem para o destino, migração pode ser total ou incremental ou a combinação dos dois tipos

## Migração de dados Heterogênea

Etapas para a migração heterogênea:

1. instância de replicação onde serão executadas as ações operações
2. definir a origem
3. definir o destino
4. converter os queries para a tecnologia de destino
5. migrar os dados da origem para o destino, pode ser migração total ou incremental ou a combinação dos dois tipos

# Schema Conversion Tools (SCT)

Serviço responsável por converter a linguagem de criação de estrutura de uma plataforma de banco de dados para outra plataforma de banco de dados auxiliando assim a diminuir os impactos dessa migração e também melhorando o tempo de inatividade de um app para essa operação. A ferramenta ainda poderá documentar os pontos onde não for possível converter automaticamente algum fragmento de código para ser visto e convertido manualmente.

Link da documentação: https://docs.aws.amazon.com/pt_br/SchemaConversionTool/latest/userguide/CHAP_Source.html

## Consolidações de banco de dados

Com a ferramenta AWS Migrations podemos consolidar mais de uma fonte de dados para um destino, exemplo: de um banco de dados local + um banco de dados RDS para um Amazon Aurora. Vale lembrar que também é possível aplicar mais de um destino para a migração de dados.



