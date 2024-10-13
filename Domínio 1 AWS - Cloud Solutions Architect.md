# Domínio 1 AWS - Cloud Solutions Architect

Armazenamento, desacoplamento, solução de arquitetura multi-nível, Alta disponibilidade e/ou tolerância a falhas.

## Volumes efêmeros

É o tipo de armazenamento que já vem por default em algumas instâncias EC2, por exemplo instância t2.micro. Esse tipo de disco é durável apenas enquanto a instância estiver em funcionamento (durabilidade no nível da instância). 

Não recomendado quando se deseja permanecer os dados após parar a instância.

## S3:

Armazenamento de objetos(algo similar ao google drive), <u>grandes volumes</u> de dados ideal para <u>backup arquivos e imagens com alta durabilidade</u>.

Acesso aos dados acontece via API, HTTP ou HTTPS.

>[!TIP] 
>Questões de prova: Durabilidade de dados, Segurança e ciclo de vida de objetos.

## Elastic File System (EFS):

Armazenamento de arquivos. Aceita multi-atach e oferece baixa latência. Ideal para compartilhamento em <u>tempo real</u>. Ideal para uso com Linux.

Pode ser acoplado aos serviços: EC2, ECS, EKS, Lambda e Fargate.

Faz sentido usar quando se deseja compartilhar arquivos entre várias instâncias Linux.

>[!TIP] 
>Questões de prova: Sistema de arquivos distribuídos e baixa latência.

## FSx:

Sistema de arquivos otimizado para Windows e Lustre, ideal para sistemas que precisam de <u>alta performance</u>. Indicado para armazenamento compartilhado.

Faz sentido quando se deseja compartilhar arquivos entre várias instâncias Windows/Lustre.

> [!TIP]
>Questões de prova: Sistemas especializados Windows e Lustre, alta performance.
> ## EBS (Elastic Block Store)

É um disco onde é possível manter os dados intactos após parar a instância. Fornece armazenamento em bloco e é anexado na mesma AZ que a instância.

Fornece persistência de longo prazo e pode ser migrado de AZ através de Snapshots.

Trabalha bem com Windows, não permite multi atach e tem diversos "tipos de EBS" que atendem diversos casos de uso.

### Tipos de disco EBS:

- **SSD de Uso geral (GP2)** - Volumes de inicialização, aplicações interativas de baixa latência, desenvolvimento, teste. De 1 a 16TB de tamanho. Máximo de IOPS 16.000. Taxa máxima de transferência de 250Mb/s. Atributo dominante: IOPS;
- **SSD de IOPS provisionado (io1)** - Para banco de dados, alto consumo de entrada e saída de dados. Tamanho de 4 a 16TB, Máximo de IOPS 64.000. Taxa máxima de transferência de 1000Mb/s . Atributo dominante: IOPS;
- **HDD Otimizada taxa de transferência (st1)** - Big data, data warehouses, processamento de log. Tamanho de 125Gb a 16TB, Máximo de IOPS 500. Taxa máxima de transferência de 500MB/s . Atributo dominante: MB/s
- **HDD a frio (sc1)** - Dados mais frios, menos acesso ao dia. Tamanho do volume de 125GB a 16TB, IOPS de 250MB/s. Taxa máxima de transferência de 250MB/s. Atributo dominante: MB/s.

>[!TIP]
>  Questões de prova: IOPS provisionado, armazenamento persistente em bloco, armazenamento de logs, armazenamento de banco de dados, disco de inicialização.