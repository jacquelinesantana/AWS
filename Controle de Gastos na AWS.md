# Controle de Gastos na AWS

Serviços e dicas para controle de gastos na AWS.

Os serviços aqui apresentados tem relação direta o *Cloud Financial Management* que faz parte do pilar de Gestão Financeira de nuvem do WellArchitected Framework. Ele tem como objetivo permitir que os clientes atinjam seus resultados de negócios da maneira mais econômica e acelerem a criação de valor econômico e de negócios, ao mesmo tempo em que encontrem o equilíbrio direto entre agilidade e controle.

Para o Cloud Financial  Management Framework na nuvem AWS teremos os seguintes pilares: veja, salve, planeje e execute.

- Veja: perguntas base: "como você está atualmente medindo, monitorando e criando responsabilidade para seus gastos com nuvens?" "Tem controle e acompanhar de onde vem os custos - aplicar as tags de forma estratégica para auxiliar a manter essa visão total e parcial dos gastos em nuvem, assim como manter a estrutura da empresa bem organizada no AWS Organizations?" Sugestão de ferramentas: AWS Control Tower. Cost Explorer, Relatórios de custo e uso da AWS, politicas de tags, Categorias de custo...
- Salvar: perguntas base: "Quais alavancas de custos você esta usando atualmente para otimizar seus gastos? Esta familiarizado com o modelo de uso e de preços?" Sugestão de ferramentas: instâncias spot do EC2, uso do Auto Scaling Groups para dimensionar sua carga de trabalho. Instâncias reservadas, Grupos de Auto scaling, planos de paupança, melhores práticas para lidar com a EC2
- Plano: perguntas base: "Como você planeja hoje os gastos futuros?" "Você tem uma metodologia para quantificar a geração de valor para uma nova migração?" Sugestão de ferramentas: AWS Cost Explorer, AWS Cost and Usage Report, AWs Bugdes, Alertas de orçamento.
- Execute: perguntas base: "Quais são alguns dos processos operacionais e ferramentas que você está usando atualmente para gerenciar sua nuvem e quem esta liderando esse processo?" "Você já pensou em como as coisas funcionaram a partir de uma perspectiva de operações diárias?" Sugestão de ferramentas: AWS Billing and Cost Management console, IAM, Service Control Polity(SPC), AWS Service Catalog, AWS Costnomaly Detection, AWS Budgets.

Conteúdo extraído de: https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/practice-cloud-financial-management.html

## Billing and Cost Management

Serviço da AWS voltado para controle e pagamentos, nesse painel teremos alguns recursos para acompanhamento de gastos, estimativa e alertar de orçamentos.

### Home

Nesta tela teremos acesso ao Custo acumulado do mês, histórico do mês passado, Monitor de custos , Detalhamento de custos, Ações recomendadas. Explorar com acalma cada um desses itens pode contribuir para melhor entendimento da saúdo financeira da sua conta AWS.

![Billing and cost management](C:\Users\tijac\Documents\aws\estudo\images\custos\1.PNG)

## Conceitos básicos

Nesse item você poderá explorar a documentação e poder da ferramenta de gestão de custos e pagamentos e suas funcionalidades. Indicamos a leitura. Um dos itens que não se pode deixar de ver ao menos uma vez são os workshops de prática de gestão financeira: https://catalog.workshops.aws/well-architected-cost-optimization/en-US, mas você também terá acesso a workshops com muitos outros itens e serviços no link: https://www.wellarchitectedlabs.com/cost-optimization/

![Billing and cost management](C:\Users\tijac\Documents\aws\estudo\images\custos\2.PNG)

## Explorador de custos

Nesse item teremos uma ferramenta que possibilita criar filtros por data, mensal, diário ou por hora dos seus custos. Além dessas opções terá acesso a outros filtros para gerar gravo ou exportar os dados para analise.

## Detecção de anomalias

É um serviço gratuito que permite criar alertas(serviço de SNS pode gerar custos) para ajudar a identificar a causa raiz dos picos de custo de uso, fornece monitores personalizados, pode ajudar recomendando otimização de recursos da AWS para dimensionar recursos EC2.

## Budgets ou orçamentos

Serviço que permite estabelecer orçamentos e te avisa com e-mail quando o seu serviço estiver próximo de estourar o orçamento ou caso já tenha estourado o orçamento.

## Calculadora AWS

Assim como diz o nome do serviço é uma calculadora que permite estimar com mais segurança e precisão o valor do uso de um determinado serviço, basicamente você vai informar os serviços que pretende contratar e o tempo de uso, ela te retorno o valor de custo para os mesmos.

## Hub de otimização de custos

Ferramenta para auxiliar a consolidar e priorizar as recomendações de orimização de custos nas contas e regiões AWS. Tras sugestões de Savings Plan, tipo de instâncias, gerenciamento de faturamento e custos...

## AWS Billing Conductor

Serviço que permite personalizar suas taxas de faturamento, exibir dados na fatura de maneira significativa para sua organização é um serviço que vai cobrar uma taxa fixa conforme a quantidade de contas que possui sua organização.

## Saving Plans

Modelo de definição de preço que oferece preços baixos para o uso da AWS, em troca de um compromisso com uma quantidade de uso(media/hora) por um período de 1 a 3 anos.

Exemplo: serviço mais caro de EC2 vai ser o que te atende sem planejamento prévio, é imediato e não requer compromisso. Segundo caso você faz um planejamento e diz que quer ficar um ou mais anos com um serviço e com isso você ganha descontos no valor do serviço. Quanto mais exato você consegue ser no seu planejamento você vai ter mais vantagens do valor porém mais restrição para alterações futura no formato do serviço(mudar região ou tipo de instância). 

Prática:

1. Você escolhe tipo de plano: 

   Compute Savings Plans - você escolhe o valor inicial e tem liberdade de escolher qualquer região, qualquer tamanho, pode ser aplicado para AWS Lambda, Fargate ou EC2.

   EC2 Instance Savings Plans - você só aplica ao EC2, para a região e família pré definida.

   SageMaker Savings Plans - sistema de aprendizado para ML
   
2. Defina o tempo de contratação de 1 a 3 anos

3. Defina o valor que você pretende gastar por hora (atenção ao definir um valor de x, ao passar desse valor o seu serviço você automaticamente passa a pagar o valor on demand)

4. Defina o tipo de pagamento(pagar tudo no ato da contratação/ Pagar parcialmente agora/ Pagar tudo mensalmente)

5. Defina o início do seu plano

6. Ao seguir e clicar no botão Submit order você já contratou o serviço


## Reservas

Painel que vai exibir os custos de instâncias reservadas e identificar oportunidades de reduzir os custos para esse serviço. Aqui você vai ter que definir o tipo de máquina que vai ser utilizado e já deixar definido a zona, e sistema operacional. Consegue ser mais barato que a Saving Plans.

Caso você não for utilizar essa maquina você pode coloca-la a venda na AWS.

Prática:

1. Para a prática você precisa ir até o serviço que será contratado, exemplo EC2
2. Procurar pelo item Reserved Instances
3. Informe o Sistema operacional
4. Informe o Tenancy (dedicado ou convencional)
5. Informar se vai querer fazer dessa reserva imutável ou não, lembrando que imutável será maior o desconto.
6. Informar o tipo de instância
7. Informar o termo/ tempo
8. Informar o tipo de pagamento
9. Enviar e ele vai enviar o valor que seu serviço vai custar. 

## Preferencias e configurações

Preferências e configurações permite definir método de pagamento, faturamento, e configurações fiscais.