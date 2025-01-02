# AWS Database Migrations Service (DMS)

Serviço que facilita a migração de dados entre banco de dados de outras fontes (outros serviços ou onpremises) para a AWS RDS. Podemos então utilizar esse serviço para fazer migração de dados homogêneas ou heterogêneas. Ou seja, podemos migrar de um banco de dados Mysql para outro banco ainda dentro da plataforma Mysql ou de um Mysql para um Postgre ou outra plataforma.

Podemos também utilizar esse serviço para migrar dados de um banco de dados na AWS para um banco de dados onpremises, e isso tudo ser feito a manter o serviço operando e ter o mínimo possível de inatividade do sistema. 

O DMS não é compativel apenas com o RDS podemos utiliza-lo para migrar dados para o S3 e ou o Redshift(warehouse) 

É possível ainda migrar entre uma estrutura SQL para uma estrutura NOSQL com auxilio do DMS.

