# Cloud AWS

Computação na nuvem é o termo que utilizamos para serviços e plataformas que estarão disponíveis fora da sua máquina local, podemos aqui ter desde sistema operacionais, servidores completos com recursos de memória Ram e Processadores tudo por conta de uma empresa que estará cuidando da parte física dessa operação. Lembrando que o tipo e tamanho do recurso serão escolhidos pelo contratante e o pagamento na maioria das vezes é conforme a demanda de utilização.

Para melhor aproveito do material, esta sendo implementado nesse momento um dicionário de termos, sinta-se a vontade em contribuir sua dúvida ou observação sobre o mesmo através da rede social: https://www.linkedin.com/in/hernandesjacque/ e/ou e-mail: ti.jacque@gmail.com ou pull request.

![On premise x cloud](./images/01.JPG)

Temos aqui alguns serviços tais como: 

- computação
- redes e entregas de conteúdos
- gerenciamento e governança
- banco de dados
- segurança, identidade e compliance*
- gerenciamento de custos
- armazenamentos

## Infraestrutura global AWS

- **Região** é um conjunto de zona de disponibilidades onde teremos um conjunto de coleção de recursos em uma localização geográfica. Exemplo o norte da Virgínia é geralmente a região onde são implementados novos recursos em primeiro momento e depois esses recursos são replicados para outras regiões. Outro dado interessante é que no norte da Virgínia temos 6 zonas de disponibilidade.

  Dessa forma teremos os novos recursos implementados primeiro nas Regiões que surgiram primeiro, e por ultimo nas regiões mais atuais.

  Outro fato importante é saber que cada região é como se um Estado, que é empregado os servidores e cada uma das regiões vão ter sempre no mínimo 2 zonas de disponibilidade para garantir redundância entre os serviços/dados nesta alocados.

### zonas de disponibilidade e regiões (outubro de 2023)

Ver site: https://docs.aws.amazon.com/pt_br/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html#Concepts.RegionsAndAvailabilityZones.Regions

- **Zona de disponibilidade estão distintos a quilômetros de distância uma das outras**, conectadas com alta velocidade, com segurança local, refrigeração e poder ser um ou mais data centers. Distância entre as zonas de até 100km. Estes são conectados para ter baixa latência, auto rendimento e redundância. Essa disposição das zonas está relacionado ao conceito e Escalabilidade.

Ao contratar um serviço AWs a ideia será sempre ver qual a região mais próximo do seu usuário. Não importando muito qual a zona de disponibilidade exatamente esta seu serviço, o foco é a região estar o mais próximo possível. Dependendo de como é configurado a sua instancia quando uma zona estiver com problemas ou indisponível a outra irá assumir o serviço. Esse modelo garantiu a AWS o título de **líder do IaaS - infraestrutura como serviço**.

- **Edge Locations** ou **PoPs (pontos de presença) ou zonas locais - são utilizados como cache de dados** é uma infraestrutura de servidores, localizado próximo de uma zona de disponibilidade, armazena dados mais solicitados no cache para melhorar latência de uma requisição de consulta. Estão em pontos estratégicos sem cobertura pela AWS. Exemplo:  **Amazon Cloud Front**, que armazena o cache do seu site estático, por exemplo. Outro serviço **AWS Lightsail** ou **AWS ElastiCache** (banco de dados em memória).

  Site: https://docs.aws.amazon.com/pt_br/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html#Concepts.RegionsAndAvailabilityZones.LocalZones
  
- **Wavelength** - permite aos desenvolvedores criar aplicativos com latências inferiores a 10 milissegundos para aplicativos mobile. Isso porque a AWS cria uma estrutura de servidores próprios dentro das companhias de internet móvel, assim a conexão acontece do celular para os equipamentos da AWS dentro da provedora de internet e desses equipamentos para os servidores onde o serviço da AWS esta hospedado.

- **AWS Outposts** - é a AWS levando sua estrutura computacional e serviços para dentro de empresas, locais de terceiros que necessitam de conexão mais rápida com os serviços.

## Seis vantagens do uso da AWS

1. **Save Money** - não gastar com manutenção de hardware
2. **Stop Guessing** - ter maior precisão de valores com investimento em tecnologias, não é necessário planejar infraestrutura que ficará obsoleta daqui algum tempo, você pode contratar um serviço menor e ir escalando conforme a demanda e acompanhamento de consumo.
3. **Variable Expenses** - você paga pelo que é utilizado e diminui a posse, é o aluguel do recurso na nuvem. Troca de despesa capital por despesa variável.
4. **Economies of Scale** - quanto mais empresas contratam um serviço na AWS mais esse recurso ficará com valor mais acessível pois a AWS "repassa" essa escala de maneira a melhorar o valor cobrado.
5. **Increase Speed and Agility** - enquanto em um rede local você demora para subir um novo serviços, na nuvem isso é resolvido em poucos cliques. Temos também facilidade em montar ambientes de testes que podem ser excluídos após os testes, por exemplo.
6. **Go Global** - Sua aplicação pode ser disponibilizada em diversas regiões no globo, diminuindo a latência do serviço. Torne-se global em minutos.

## Arquitetura AWS

A arquitetura que atendem os serviços da AWS estão baseados em 3 camadas:

- **Presentation tier (apresentação)**: é a camada mais próxima do usuário, pode ser a camada de front end no caso de uma aplicação web, ou o Cloudfront no caso de um servidor de conteúdos. Para essa camada teremos o Amazon Cognito(serviço de login), o Cloudfront, Aws Amplify(ferramenta para front-end) e Route 53.
- **Logic Tier (lógica)**: é a camada de regras de negócio e/ou crud por exemplo, é a segunda camada após a mais próxima do usuário. como um bucket do S3 ou o backend de uma aplicação web. Para essa aplicação temos como exemplo os serviços de AWS Lambda, Amazon e Api Gateway
- **Data Tier(Dados):** é a camada mais distante do usuário, geralmente pode ser um banco de dados onde o que foi processado pelo backend será armazenado.

![Arquitetura AWS](./images/02.png)

![Exemplo de uma aplicação web na arquitetura AWS](./images/05.JPG)

## Responsabilidade compartilhada

É o conceito onde a AWS assume a sua parte de responsabilidade no serviço e o Arquiteto/ ou pessoa responsável pela implementação dentro da empresa ficará responsável pelas configurações e toda a parte que lhe cabe. 

A plataforma que oferece os serviços fica responsável pela manutenção do hardware, atualizações entre outros...

O contratante fica responsável pela segurança da sua parte, escolha pelos produtos e gerenciamento, por exemplo. Lembrando que quase tudo pode ser gerenciado a adaptado conforme a demanda. A seguir vamos retomar o assunto deixando mais nítido as responsabilidades diante de cada modelo de serviço ofertado pela AWS.

**Para o cliente** - Responsavilidade IN the cloud (na nuvem) a responsabilidade do contratante é definir as tecnologias, escolher formas de criptografia, escolher tipo de rede, configurar serviços e segurança, níveis de acesso e grupos de usuários...

**Para a AWS** - responsabilidade OF the cloud (responsabilidade da nuvem). Responsável por suportar os serviços, manter a estrutura computacional, regiões e zonas de disponibilidade.

## IaaS, SaaS e PaaS

**IaaS** - infraestrutura como serviço é o modelo computacional que entrega toda a estrutura que seria física (servidores, redes, cabeamentos, segurança de rede) - Amazon EC2 você consegue criar e gerenciar instâncias computacionais, onde nela vc terá o ambiente necessário para executar suas aplicações. Essas instâncias é um computador virtual onde pode-se definir a sua estrutura e rodar nesse ambiente suas aplicações. O objetivo desse serviço será tirar das mãos do contratante a preocupação com a parte física de um servidor. Mas aqui ainda temos como responsabilidade do contratante escolher a melhor tecnologia, serviço operacional e outros e também manter as devidas atualizações do sistema operacional e demais recursos que ele optou em utilizar em seu servidor.

**PaaS** - Plataforma como serviço, a diferença aqui é que não fica mais sob a responsabilidade do contratante atualizações de sistemas operacionais, por exemplo. O foco é na implantação e gerenciamento das suas aplicações, exemplo: AWS Elastic Beanstalk, esse é um serviço que facilita a implantação e o gerenciamento de aplicativos web e serviços na nuvem, aqui você não se preocupa com configuração de servidores, redes, balanceamento de carga e escalonamento, você só precisa se concentrar em desenvolver seu aplicativo e fazer o upload do código.

**Saas** - Software como serviço aqui o produto é completo, exemplo Gmail, você só utiliza o serviço não precisa se preocupar nem com a infla estrutura nem com a tecnologia da aplicação.

### Recurso Gerenciados

É ter como responsabilidade da AWS a infraestrutura e todos os recursos que te permitem utilizar um serviço de banco de dados.  Exemplo: precisando de um banco de dados em nuvem, podemos contratar o serviço de EC2, criar uma instancia neste e ficar responsável por toda configuração do ambiente e atualizações para o funcionamento do banco de dados ou podemos contratar apenas o serviço de banco de dados e deixar a AWS responsável por tornar este funcional e disponível.

Um recurso deixa de ser gerenciado por você e quando a outra parte inicia o gerenciamento, atualizações e manutenção do sistema operacional e a segurança.

Para ficar mais nítida a diferença desses serviços veja quais são as responsabilidades de cada camada para cada um dos modelos computacionais:

- **Modelo tradicional on Premises** - Responsabilidade da empresa contratante são as camadas de:

APP | Dados | Sistema Operacional | Servidores | Armazenamento | Rede

- **Modelo IaaS** - Responsabilidade da empresa contratante são as camadas de:

APP | Dados | Sistema Operacional

- **Modelo PaaS** - Responsabilidade da empresa contratante são as camadas de:

APP | Dados

- **Modelo SaaS** - Responsabilidade da empresa contratante são as camadas de:

nada apenas utilizar o serviço

| Modelo computacional               | Responsabilidade do Cliente                                  | Responsabilidade AWS                                         |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Modelo tradicional on Premises** | Infraestrutura<br />Rede<br />Computadores/Servidores (escolha e implementação)<br />Sistema Operacional<br />Firewall<br />Tratamento para Antivírus e invasões<br />Manutenção de Hardware<br />Manutenção e atualização de software<br />Manutenção de atualizações de programas<br />Segurança física<br />Segurança online<br />Backup<br />Chaves para os programas originais<br />Ter que pagar por uma nova estrutura caso precisar atender mais de uma região. | -                                                            |
| **Modelo IaaS**                    | Escolha de Sistema Operacional<br />Escolha de recursos de hardware/recursos<br />Escolha de estrutura de segurança<br />Manutenção de Softwares que forem implementados<br />Atualizações de software<br />Manutenção de atualizações de programas<br />Segurança online<br />Backup<br />Licenças dos programas (caso optar)<br />Escolha da região onde deseja ser atendido<br />Replicar serviços em mais de uma região sem custo de hardware, prédio... | Infraestrutura<br />Rede<br />Computadores/Servidores (escolha e implementação)<br />Segurança física |
| **Modelo PaaS**                    | Escolha de recursos de hardware/recursos<br />Escolha de estrutura de segurança<br />Segurança online<br />Escolha de melhor solução<br /><br />Configuração de backup e redundância<br /><br />Atualizações dos programas implementados<br />Replicar serviços em mais de uma região sem custo de hardware, prédio... | Infraestrutura<br />Rede<br />Computadores/Servidores (escolha e implementação)<br />Segurança física<br />Manutenção e implementação de Sistema Operacional <br /><br />Licença do Sistema operacional (caso optar) |
| **Modelo SaaS**                    | Escolha de melhor solução<br /><br />Seu código e segurança de acesso ao painel AWS | Infraestrutura<br />Rede<br />Computadores/Servidores (escolha e implementação)<br />Segurança física<br />Manutenção e implementação de Sistema Operacional <br />Manutenção e implementação da solução operando para ser apenas utilizada<br />Licença dos programas (caso optar)<br />Backup automático<br />Redundância automática |

![Responsabilidade compartilhada](./images/03.gif)

## IAM - Identity And Access Management

Recurso para gerenciar os acessos e identidades no seu ambiente AWS, implementando segurança ao ambiente. Aqui podemos ter práticas que levam a uma maior segurança assim como algumas práticas também podem ser muito perigosas para o mesmo.

O ideal para esse item, que pode ser considerado um item de segurança é que cada usuário tenha sua conta registrada e vinculada ao painel root que vai ser o dono do painel, vamos ver a seguir as boas práticas para o IAM e também como adicionar contas e configura-las entro do painel da AWS. Possui padrão PCI DSS de conformidade que é um padrão de requisitos necessários para segurança utilizada nas transações de cartão.

### IAM - dicas

O Iam é o serviço que permite gerencias usuários e grupos de usuários da sua conta, algumas dicas que devemos nos atentar:

- **Usuários possuem credenciais permanentes** e **funções possuem credenciais temporárias**
- Usuários root não devem ser compartilhados
- Use o **Least Privilege Principle** nos usuários - mínimo de privilégios necessários
- Documentos Json definem as permissões de acesso
- Grupos contém outros usuários, mas não podem conter outros grupos
- Utilizar Multifator Authentication (MFA)
- Criar politica para a criação de senha das contas associadas a root
- É um serviço gratuito da AWS
- Bloquear as chaves de acesso do usuário root
- Criar usuários individuais do IAM
- Criar grupos para atribuir permissão
- Ver sobre conceitos básicos de uso de permissões com políticas gerenciadas
- Usar políticas gerenciadas pelo cliente em vez de políticas gerenciadas em linha
- Use níveis de acesso para revisar permissões
- Use funções para aplicativos que são executados em instâncias do CS2
- Use funções/roles para delegar permissões 
- Troque de credenciais regularmente
- Remova as credenciais desnecessárias
- Monitorar as atividades em sua conta
- Integração com diversos serviços
- Para a conta root, definir aos seus usuários uma política de senha forte.

![IAM](./images/04.JPG)
> [!IMPORTANT]  
>Primeiro autentica - depois autoriza**
> **Usuários** - pessoa ou serviço, com credenciais permanentes. Use o Least Privilege (privilégio mínimo)
> **Federated Users** - login por facebook e outros
> **Grupos** - coletivo de usuários (grupos não podem conter outros grupos)
> **Funções/roles** - não são permissões é um método de autenticação temporária.
> **Politica** - Através das politicas é possível permitir que serviços acessem outros serviços ou recursos dentro da AWS.
> <u>Através desses você consegue criar e gerenciar Politicas IBP ou RBP</u>

### Politicas de acesso

Politicas de acesso pode ser definidas para usuários, Grupo de usuário e para role(função)

Temos a **politica in line** que pode ser aplicada a um usuário ou uma role.

Temos também o **AWS Managed** e o **Custumer Manager** que pode ser aplicada ao usuário, grupo ou role.

Essas Três modalidades não afetam o resultado final e podem ser localizadas no serviço IAM.

- **Identity Policy** - São politicas que são aplicadas a usuário(s) e ou grupo(s)
- **Resource Policy** - São politicas que são aplicadas/associadas a recursos - Exemplo  EC2, S3...

Politicas são escritas em Json:

```
"Statement":
[
    {
        "Effect":"Allow",
        "Action":[
            "s3:GetBucketLocation",
            "s3:ListAllBuckets"
        ],
        "Resource":"Arn:aws:s3:::*"
    },
    {
        "Effect":"Deny",
        "Action":"s3:*",
        "Resource":[
        "arn:aws:s3:::YOUR-BUCKET",
        "arn:aws:s3:::YOUR-BUCKET/*"
        ]
    }
]
```

O Json de uma policy pode ser do tipo **Deny** (negação) ou **Allow**(liberar) conforme a necessidade de liberar ou bloquear o acesso ao serviço/recurso, essa informação estará em **Effect**.

Em **Action** teremos o recurso que vamos aplicar a politica, no exemplo acima estamos no primeiro objeto do Json passando que o S3 terá o Get da localização do bucket local permitido, por exemplo.

Em **Resource** teremos para quem será aplicado essa politica, no caso do segundo objeto do Json estamos aplicando ao seu bucket e a todos os recursos dentro do seu bucket.

Poderíamos ter um **Condition** também para dar condição da politica, por exemplo definindo para quais S3 vamos seguir essa politica.

### Security Group (Grupo de segurança)

- São como firewalls virtuais que controlam o tráfego de entrada e saída de suas instâncias EC2 e outros serviços da AWS que envolvem recursos de rede como: Elastic Load Balancing, Elastic Container Service, RDS.
- Posso aplicar a uma instância permitindo o acesso a partir de outra instância a uma porta específica tornando tudo mais seguro, uma vez permitido o acesso ele libera a saída para o mesmo.
  - Controle granular de tráfego permitindo ou bloqueando acesso específico para portas e protocolos
  - Segurança por instância: cada instância pode pertencer a um ou mais grupos de segurança
  - Flexibilidade: configure regras de forma rápida e fácil.
- Uso de grupos de segurança tornar as regras mais consistentes já que pode-se aplicar mesmo grupo a várias instâncias, RDS, Containers...

### ALC (Access Control List - Lista de controle de acesso) Não indicada para EC2

- São documentos Json que definem as permissões de usuário, grupo ou papel(role) na AWS
  - Controle de acesso a serviços: define quais serviços da AWS um usuário pode acessar e quais são ações que ele pode realizar.
  - Gerenciamento de identidade: Associe políticas a usuários, grupos ou roles para controlar o acesso aos recursos.
  - Segurança baseada em identidade: Garanta que apenas usuários autorizados possam realizar determinadas ações.
  - Aplica-se para Buckets e sub-redes

Aplicar uma Regra a lista da VPC:

1. No serviço VPC buscar por Network ACLs
2. Selecionar a ACL para seu vpc ou criar uma nova ACL
3. Ao adicionar as regras de entrada/ saída você precisa cuidar sempre das duas pontes - entrada e saída pois as regras não se estendem. Se você configurou regra apenas para a entrada a saída ficará sem regras associadas.
4. Número da regra é sobre a ordem em que as regras vão ser atendidas
5. Tipo você define para qual ação vai se aplicar a regras ICMP - ping por exemplo
6. Origem, é o ip da máquina onde vamos aplicar a regra
7. Permitir/negar é para definir se estamos liberando essa ação ou limitando.
8. ![ACL](./images/53.png)

### Roles(funções)

- São entidades AWS que podem assumir permissões temporárias.
  - Delegar privilégios: conceder permissões a serviços ou outros usuários sem compartilhar credenciais
  - Acesso temporário: Criar roles com permissões específicas para tarefas específicas.
  - Integração com outros serviços: Utilize roles para permitir que serviços como o EC2 assumam um papel e acessem outros recursos

### Diferenças entre Grupos de segurança e ACL 

- **Grupos de segurança: segurança em rede para EC2 e outros serviços relacionados a redes**
- **Politicas IAM: controlar ações que usuário podem realizar** 
- **Roles: Permitir a delegação de privilégios de forma segura**

> [!TIP]
> O Security Group é StateFull então se vc cria a regra de entrada você não precisa criar as regras de saída.
> A ACL é StateLess. Nesse caso precisamos criar as regras de entrada e saída.

### Security Token Service(STS)

Permite que você solicite tokens de sessão do endpoint global que funciona em todas as regiões da AWS. É um serviço global e todas as solicitações de STS vão para um único endpoint em https//sts.amazonaws.com.

> [!IMPORTANT]  
>
> - **Reduza a latência** - fazer as chamadas do STS para o endpoint que esteja mais próximo
> - **Construir em redundância** - usar isolamento de falhas para proteger sua carga de trabalho
> - **Aumentar a validade do token da sessão** - Token gerado regionalmente para um serviço é diferente de token global para a mesma aplicação/serviço.

### Como criar uma função/role de permissão de acesso a uma S3 em uma instância EC2

1. No IAM clicar na opção Role ou função do menu
2. Clicar em criar função
3. Selecionar opção Serviço da AWS
4. Selecionar opção EC2
5. Opção EC2,allows EC2 instances to call AWS services on your behalf
6. Botão próximo
7. Informar qual o o objetivo do role/função exe: S3 full Access ou S3 Read Only Access
8. Botão próximo
9. Dar nome de fácil identificação da função
10. Clicar em criar

## Controle de usuários

### AWS Organizations

Ferramenta para gestão e controle de gastos e usuários com setorização, oferece governança, segurança e automação.

- Governança e conformidade: Políticas centralizadas de segurança e conformidade, reduzindo riscos de desvios e facilitando auditorias
- Controle de serviços: limite os serviços que podem ser acessados por diferentes contas ou grupos, garantindo que apenas os recursos necessários estejam disponíveis.
- Gerenciamento de tags: Utilize tags para organizar e classificar seus recursos, facilitando a análise e a aplicação de políticas.
- Criação automatizada de contas aplicando automaticamente configurações e políticas predefinidas
- Integração com outros serviços como CloudFormation, para automatizar a implantação de recursos em toda a sua organização
- Gerenciamento de ciclo de vida de contas garantindo que sua infraestrutura esteja sempre alinhada com as suas necessidades
- Estrutura hierárquica pra contas
- Delegação de responsabilidades de adm para diferentes equipes ou departamentos sem comprometer segurança
- Escalabilidade adaptar sua organização à medida que sua empresa cresce adicionando ou removendo contas
- Integração com o AWS Config, AWS CloudTrail.
- Utilizar o IAM para definir as permissões de usuários e grupos dentro da organização
- Controle de acesso baseado em atributos dos usuário como o departamento ou tags relacionadas

### Service Control Policy

Para aplicar restrições em várias contas-membro, você deve usar Service Control Policy(SCP) na Amazon Organization, assim pode-se criar uma regra de negação que se aplique a qualquer coisa, exemplo restringir o uso de algum tipo de instância EC2.

### AWS Resource Access Manager (RAM)

Ajuda a compartilhar seus recursos com segurança entre diferentes contas AWS, dentro de sua organização ou unidades Organizacionais(UOs) e com perfis e usuário do IAM para tipos de recursos compatíveis.

## Interfaces de acesso AWS 

1. **AWS Management Console** - é o sistema da AWS acessado por navegador ou por celular com o aplicativo AWS Console Mobile APP.
2. **Command Line Interface (CLI)** - Prompt de linha de comandos, suporte para Linux, Power Shell..
3. **API** - As aplicações acessando os serviços da AWS, pode ser uma aplicação já alocada dentro da AWS que se comunica com outros serviços AWS. Exemplo: backend se comunicando com banco de dados.
4. **Software Development Kit (SDK)** - Este permite que se utilize um conjunto de linguagens de programação que pode ser PHP, Javascript, Java entre outras para se comunicar com a sua aplicação.

## Computação

Serviços computacionais em nuvem, diz respeito a locação de máquinas/ servidores, onde podemos ter controle total de sistema operacional, versão, atualizações de Sistemas e outras aplicações ou ainda podemos apenas locar o espaço que vai ser hospedagem para aplicações, transferindo preocupações com o hardware e até mesmo podemos transferir as preocupações com atualizações de sistemas para a AWS, focando assim, na aplicação final. Abaixo vamos ver alguns serviços considerados serviços de computação:

### EC2

![EC2 - instâncias](./images/06.gif)

Serviço que permite criar instâncias computacionais, que podem ser comparadas com um computador virtual onde definiremos as configurações de hardware e vamos ser responsáveis pelo sistema operacional e toda a estrutura computacional, ficando a AWS responsável pela parte física. (**IaaS**) | `aplicação`: quando se quer ter mais autonomia sobre o servidor ** principal produto

- Dentro desse serviço teremos alguns tipos de inicializadores (ou Launch Types) que estão em 4: **Sob Demanda**; **Instâncias Spot**; **Instâncias Reservadas**; **Host e Instancia Dedicada**:

  - **On Demand - Sob Demanda**: alto custo se utilizado a longo prazo - aplica-se a projetos de curto prazo, cobrança é realizada conforme o uso, não tem compromisso de uso, não se aplica pagamento adiantado, Pode-se aumentar ou diminuir a capacidade computacional a qualquer momento. 

 > [!TIP]
  > *Aplica-se quando possui cargas de trabalho de curto prazo, validar hipóteses, com pico de utilização imprevisível, testar e experimentar um ambiente*;
  > *TAMBÉM TEM A POSSIBILIDADE DE CRIAR UMA INSTÂNCIA SOB DEMANDA RESERVADA PARA MELHORAR O CUSTO, DEFININDO HORAS TRABALHADAS E PERÍODO.*

  ![On Demand](./images/07.jpg)

  - **Instancias reservadas**: Até 75% de desconto em comparação ao modelo por demanda, aplicações que exigem capacidade reservada, comprometimento de uso da instância por um período de 1 ou 3 anos, possui pagamento adiantado;

 > [!TIP]
  > *Aplica-se para ambiente de produção que foi testado e não será modificado, aplicações que precisar ser estado constante, excelente para banco de dados*;
  > Podem ser de dois tipos:
  >  - Standard RI - permite alterar AZ, Instance size, Networking type ($)
  >  - Convertible RI - permite alterar AZ, Instance size, Networking type, Family, OS ($$)

  ![Instâncias Reservadas](./images/08.jpg) 

  - **Spot Instances**: até 90% desconto comparado a instâncias sob demanda; São terminadas quando o preço spot, é maior do que o preço que você estabeleceu para pagar; Memorize como leilão de instâncias; terminate = preço spot da AWS>seu preço; não utilize para trabalhos críticos e banco de dados

 > [!TIP]
  > *Aplica-se quando você tem urgência de grande capacidade computacional, workloads que podem parar e serem iniciados novamente, trabalhos em lote, análise de dados, processamento de imagens.*
  > Utilizada para testes e em alguns casos ela é utilizado como Auto Scale

  ![Instância Spot](./images/09.jpg)

 - **Host Dedicado**: Hardware dedicado, servidor físico E2C Exclusivo para você, cumprir requisitos de conformidade, visibilidade de soquetes/ núcleos/Ids de hosts, Comprometimento por um período de 3 anos, pode ser comprado sob demanda de horas, se optar por reserva até 70% de desconto em comparação com instâncias por demanda;

 > [!TIP]
  > *Aplica-se quando deseja vincular licenças de software, como Windows Server, SQL Server e Suse Linux Enterprise Server. Podemos citar exemplos de casos de aplicação onde os requisitos de conformidade são mais rigorosos(PCI DSS, HIPAA...) garantindo maior segurança e reduzindo riscos de vazamento de dados,  Cargas de trabalho altamente sensíveis- informações confidenciais*. 

- Um host dedicado EC2 é um servidor físico dedicado exclusivamente a uma única conta AWS.
 - Isso significa que você tem controle total sobre o hardware subjacente e não compartilha recursos físicos com outras contas AWS.
 - Os hosts dedicados são uma opção quando você precisa de um alto nível de isolamento para atender a requisitos específicos de conformidade ou segurança.
 - Eles podem ser caros, pois você paga pela capacidade do host dedicado, independentemente de quantas instâncias EC2 são executadas nele.

  ![Host Dedicado](./images/10.jpg)

  - **Instância Dedicada**: Hardware dedicado a sua empresa, pode ser  compartilhado com outras instâncias na mesma conta, não tem controle sobre o posicionamento da instância(você só pode movimentar o hardware se interromper e reiniciar), comprometimento por um período de 3 anos
  
    * para a instância dedicada, não teremos visibilidade de soquetes, núcleos e ids dos hosts, nem afinidade entre um host e a instância, nem inserção de instância específica nem como adicionar capacidade usando uma solicitação de alocação. 

  > [!TIP]
   > *Aplica-se Quando se tem várias cargas de trabalho em uma única conta e deseja garantir um nível mais alto de isolamento entre essas cargas de trabalho, mas sem isolamento completo; economizar com a contratação de novo host dedicado, afinal se paga pela instância;  quando se utiliza uma carga de trabalho que exige uma grande quantidade de recursos em picos e não o tempo todo.* PODE-SE TER UMA INSTANCIA DEDICADA NO SEU HOST DEDICADO.

- Uma instância dedicada EC2 é uma instância de máquina virtual (VM) que é executada em um host dedicado.
- Embora a instância compartilhe o host dedicado com outras instâncias, essas instâncias pertencem à mesma conta AWS.
- Isso fornece um nível mais alto de isolamento em comparação com as instâncias EC2 padrão, que podem compartilhar hardware com outras contas AWS.
- As instâncias dedicadas EC2 são úteis quando você deseja garantir que suas VMs estejam em um ambiente mais isolado, mas não precisa de um host dedicado completo.
- O custo de uma instância dedicada EC2 é geralmente menor do que o de um host dedicado, pois você paga apenas pelas instâncias que utiliza.
  
  ![Instância Dedicada](./images/11.jpg)

> [!TIP]
> Possui famílias/ tipo de instancia para melhor atender casos e necessidades, exemplo: 
> **Família A**,T,M,MAC para uso geral, servidores, homologação e repositórios de códigos. 
> **Família C** para computacional, modelagem científica, servidores de jogos ou anúncios e marchine learning.
> instancia **T2.@xLarge** podemos entender que **T** tipo da instancia **T**= família **2** = geração, **xLarge** = tamanho
> Resumo: **banco de dados - instância reservada**; **trazer sua licença on premisse para a AWS - Host dedicado**; **Ambiente de teste por curto período, picos de acesso ou homologação - Sob demanda**; **Computação extra - Instâncias Spot**;

#### Amazon EC2 Auto Scaling

- serviço que ajuda a garantir que o contratante tenha a quantidade certa de servidores virtuais (instancias) em funcionamento para lidar com a carga de trabalho do seu aplicativo de forma automática. Então você pode definir politicas de quando o servidor deve aumentar o seu potencial de entrega e quando deve voltar ao número normal de instancias atendendo. Dessa forma se a demanda aumentar ele automaticamente vai incluir novos servidores/ instancias para atender essa demanda, se a demanda cair ele vai eliminar o número excedente de servidores para manter um melhor custo para o contratante. Ele monitora as métricas e desempenho das instancias.

![Auto Scaling](./images/12.jpg)

#### Application Load Balancer (ALP)

O Application Load Balancer é um recurso da AWS que trabalha em conjunto com o Auto Scaling, isso porque não adianta apenas subir mais máquinas temos que ter um gestor que direcione as cargas e distribua de forma a ser autossustentável as requisições entre os servidores disponíveis. Então esse gestor é o ALP.

Uma vez que aplicamos esse serviço em nossa estrutura teremos:

- Distribuição de carga - ele vai distribuir as requisições conforme configurações.
- Alta disponibilidade - caso um servidor falhe ele vai automaticamente passar as requisições para outro host.
- Roteamento inteligente - ele pode redirecionar os clientes conforme diversos critérios a serem avaliados como IP do cliente, cabeçalho da requisição, requisição...
- Segurança: O ALB oferece recursos de segurança com terminação TLS/SSL que criptografa o tráfego entre seus clientes e servidores.

![Application Load Balancer](./images/38.png)

#### Segurança no EC2

1. criar uma política de segurança(role/função) de acesso
2. criar a instancia 
3. selecionar a instancia 
   1. ir na opção ações
   2. opção segurança
   3. opção modificar função do IAM
4. escolher a role/função que precisa aplicar
5. botão atualizar função do IAM

> [!TIP]
> Evite uso de chaves de acesso, usar Role

#### Criar a função/role de acesso ao  EC2

1. no IAM clique em role ou função
2. clicar em criar função
3. selecionar opção de serviço da AWS
4. selecionar EC2 "Allows EC2 intaces to call AWS services on your behalf"
5. botão próximo
6. falar qual o objetivo da role exemplo: acesso ao S3x
7. selecionar opção Amazon S3 full Access ou S3 Read OnlyAccess
8. botão próximo
9. dar nome de fácil identificação
10. clicar em criar

#### EC2 Saving Plans

Aqui vale lembrar que é um serviço que pode ser associado ao EC2, mas que também atende outros serviços. É um contrato de 1 a 3 anos que se aplica ao serviço de EC2, precisa especificar região, família, Qualquer tamanho e Sistema Operacional. 

Esse tipo de contrato pode ser aplicado a um serviço Fargate, Lambda, EC2 - **Compute Saving Plans**. onde conseguimos aplicar a qualquer região e alterar a região, Família, tamanho e Sistema Operacional.

Já o contrato **EC2 Saving Plans** é exclusivo para EC2 apenas e pode não tem flexibilidade na região, tipo de família, tamanho ou Sistema Operacional.


#### Estado da instância

- inicia a instancia verifica IAM e fica em Pending -> Running
- de Running podemos dar um shutdown -> Terminated
- De Stopping ela vai para Stopped
- Stooped -> Pending -> Running ou Terminated

![Estados de uma instância](./images/13.gif)

#### Posicionamento de EC2

Temos 3 opções em placement group

- **Cluster** - Região, AZ, monta a EC2 uma próxima a outra quase sempre no mesmo rack - melhor latência por estar no mesmo rack, alta taxa de transferência - aplica-se para Big Data e Aplicações paralelas.

  ![Grupo de colaboração Cluster](./images/14.jpg)

- **Spread** (Espelhar/Disseminar)  -  Região, AZ, monta a EC2 em racks diferentes - aplicações que precisam de alta disponibilidade e são críticas onde a falha de uma instância não deve afetar outras instâncias.

  ![Grupo de colaboração Spread](./images/15.jpg)

- **Partition** (partição) -  Região, AZ, monta a EC2 em racks diferentes - útil para cargas de trabalho grandes e distribuídas, como Hadoop, HDFs e Cassandra, pois ajuda a reduzir o risco de falhas correlacionadas.

  ![Grupo de colaboração Partition](./images/16.jpg)

#### Redes - Comunicação entre EC2

| Rede                                      |                          Descrição                           | Representação_______                                         |
| ----------------------------------------- | :----------------------------------------------------------: | ------------------------------------------------------------ |
| **ENI**                                   | Elastic Network Interface - Podemos conectar a várias subnets da mesma AZ(zona de disponibilidade), mas não consigo conectar em uma subnet de outra AZ. Possui IP privado e um público opcional. É um dispositivo de rede virtual que fornece uma interface de rede para a EC2. Todo ENI utiliza ENA para oferecer um desempenho superior | ![ENI](./images/17.png)                                      |
| **ENA**                                   | Elastic Network Adapter - Mais rápida que a ENI atende alguns tipos de instâncias ( tem ip privada e público opcional) | <img src="./images/17.png" width="100%">                     |
| **EFA**                                   | Elastic Fabric Adapter - Utilizada para altar velocidades como Machine Learning - disponível para alguns tipos de instâncias (tem ip privado e público opcional). Principal característica é que fornece suporte a vários protocolos de comunicação como o RDMA(remote direct memory access), que permite acesso direto a memória de outras instâncias. | ![EFA](./images/19.png)                                      |
| **NAT**                                   | Network Adress Translate - Tradução de Endereços de Rede, é uma técnica de rede que permite múltiplos dispositivos em uma rede privada compartilhem um único endereço IP público para acessar a internet. Uso para quando o número de ips públicos é limitado, oculta o ip privado do equipamento, | ![NAT](./images/20.png)                                      |
| **IP Elástico**                           | É uma configuração de IP que permite reiniciar a máquina e não perder o IP público. Permite também migrar esse IP para outra máquina(OBS: ao terminar uma instância deve-se apagar o IP público caso não vá reutilizar para não gerar custos.) Oferece instabilidade, acesso remoto consistente. Ajuda em Load Balancers, para ajudar a distribuir o tráfego entre várias instâncias. | <img src="./images/21.gif" alt="Ip Elástico" style="zoom: 100%;" /> |
| **Subnet pública**                        | Tem saída para internet com o IGW internet Gateware. A EC2 localizada em uma subnet pública pode se conectar com a internet sem necessidade de um dispositivo NAT. Utilizada para servidores Web, Balanceador de carga e serviços que devem ser acessados via Web. | ![Subnet Pública](./images/22.gif)                           |
| **Subnet privada**                        | Não tem saída para internet diretamente, mas pode ter esse acesso através de um Bastion Host. | ![Subnet Privada](./images/23.gif)                           |
| **Bastion Host ou Host Jump ou Jump Box** | Utilizado como ponte de conexão instâncias de subnet privada. Essa instância é criada com Ip Público, configuramos a instância de IP Privado VPC(Virtual private Cloud), para ter acesso SSH e ou RDP ao Bastion Host. Por último configura-se o Bastion Host para um NAT Gateware, com as regras de acesso e fazendo uso apenas do consumo da internet sem se tornar disponível na internet (para as instâncias de Ip Privado) | ![Bastion Host](./images/24.png)                             |
| **Internet Gateway**                      | É bidirecional, permite o acesso da máquina a internet, mas também permite terceiros acessarem essa máquina a partir da internet. | ![Internet Gateway](./images/25.png)                         |
| **Emparelhar**                            | É possível criar um emparelhamento de VPC entre suas próprias VPCs ou com uma VPC em outra conta AWS mesmo estando em outra AZ | ![Emparelhar VPCs](./images/27.png)                          |
| **Private Link**                          | Fornece conectividade entre nuvens e serviços compatíveis AWS e sua rede on-premises sem expor o trafego na internet pública. | ![Private Link](./images/31.png)                             |
| **AWS Direct Connect**                    | Conexão física entre rede local on premises e AWS, tráfego seguro e rápido ideal para migrar grande quantidade de dados. | ![Direct Connect](./images/32.png)                           |
| **Site to site**                          | Conexão virtual via túnel entre sua rede e a AWS, estende a rede on premises para nuvem. Pode ter maior latência que o PrivateLink. | ![39](./images/39.png)                                       |

#### Cobranças no EC2

> [!IMPORTANT]  
>1. Instância em Status Stopping - não gera cobrança da instância mas cobra pelo armazenamento dos seus dados e sistema operacional (armazenamento)
>2. Endereço de IP privado mantem-se o mesmo quando a máquina esta em Status Stopping porem o ip público será perdido a menos que seja um IP Elastico
>3. Instância em Status Hivernatting - você paga pelo volume armazenado e também pela memória Ram que ainda esta ativa

#### Características de uma VPC (Virtual Private Cloud)

- podem ter subnets 
- roteamento -> tabelas de roteamento
- segurança -> grupos de segurança e lista de controle de acesso de rede(ACLs)

Gateways e Endpoints

- Internet Gateway
- Nat Gateway Instance
- VPC Endpoint - para conexão privada e seguras a serviços AWS sem passar pela internet pública

Conectividade:

- **VPN(rede privada na internet) Gateway** - permite conexão segura entre sua VPN e seu data center ou rede corporativa, cria um túnel criptografado entre duas redes, o que permite estender uma rede local para a nuvem.
- **Direct Connect** - proporciona uma conexão de rede dedicada entre sua infraestrutura local e a AWS

Benefícios:

- isolamento - proporciona maior segurança
- controle - pode-se incluir seleção de IPs, criar subnets configurar tabela de roteamento e outras configurações
- escalabilidade - pode-se ajustar o tamanho e a configuração da VPN
- segurança - regras de segurança granular permitem proteger suas instâncias.

![VPC e VPN](./images/26.png)

> [!TIP]
> #### Escalabilidade Vertical
>
> Aumentar a capacidade de sua máquina, atribuindo a esta maior poder de processamento(mais processadores, mais memória Ram, rede e dados.
>
> #### Escalabilidade Horizontal 
>
> Aumentar a quantidade de máquinas atendendo.
>
> #### Balanceamento de carga
>
> responsável por realizar a escalabilidade horizontal.
>
> #### Balanceamento de rede
>
> Qual a porta e endpoint que vai entregar, alvos que vai entregar os dados.
>
> #### Balanceamento de aplicação
>
> Ele abre o pacote e baseado em um conjunto de regras pré definidas ele vai entregar isso a uma instância ou outra, ou a um S3...



## Armazenamentos S3

**Amazon S3** (Amazon Simple Storage Service) - é um serviço de armazenamento de objetos da AWS que permite armazenar e recuperar grandes quantidades de dados de maneira simples e escalável. Oferece local seguro e confiável para armazenar qualquer tipo de arquivo e dados de aplicativos... nessa estrutura os arquivos são chamados objetos e eles estarão organizados em recipientes chamados bucket. | `Aplicação`:  pode ser utilizado como: **Armazenamento de arquivos**, **Acesso e compartilhamento**, **Escalabilidade** pois podemos lidar com qualquer quantidade de dados, **Backup e recuperação**. ** produto principal (**SaaS**)

Para o serviço S3 temos alguns tipos de classe de armazenamento que podem ser escolhidos conforme a necessidade do cliente, melhor performance ou melhor custo.

Para esse serviço a **AWS é responsável pela segurança da nuvem, proteção da infraestrutura e fornecer serviços que podem ser utilizados com segurança**, esta segurança e regularmente testada por auditores de terceiros.

Para esse serviço você é responsável pela segurança na nuvem, confidencialidade de seus dados, requisitos da sua organização, leis e regulamentos aplicáveis. Você deve:

1. Gerenciar seus dados, propriedade de objetos e criptografia

2. Classificar seus ativos
3. Gerenciar o acesso a seus dados com as funções do IAM

4. Habilitar controles de detecção como o AWS CloudTrail ou Amazon GuardDuty

Dicionário do S3:

| Serviço     | Descrição                                                    |
| ----------- | ------------------------------------------------------------ |
| **buckets** | é o local onde estará armazenado seus objetos/arquivos/dados, tal qual um drive do seu computador ele tem um endereço, pode ser de acesso publico ou restrito |
| **Objetos** | tudo que podemos armazenar em um bucket é chamado objeto (fotos, arquivos, dados, backups, etc) |
| **Keys**    | referencia ao objeto dentro do bucket, essa key vai sempre indicar o **diretório + objeto** |
| **Regiões** | o serviço S3 é um **serviço regional** com visão global, ele é criado em uma região, pode ter redundância ou não dentro dessa região, mas ele é visto de dentro do ambiente AWS globalmente, por esse motivo seu bucket deve ter nome único. |
| **ARN**     | Nome do recurso da Amazon - todo objeto que é alocado em um bucket recebe seu ARN<br />exe: arn:aws:s3:::nomeConta/nomeArquivo.png |
| **RRS**     | Reduced Redundancy Storage é uma opção de armazenamento do Amazon S3 que permite aos clientes armazenar reproduzíveis e que não sejam de fundamental importância com níveis de redundância mais baixo do que o armazenamento padrão do Amazon S3. Ela armazena objetos em vários dispositivos em diversas instalações, oferecendo durabilidade 400 vezes maior que a de uma unidade comum, mas não replica objetos tantas vezes quanto o armazenamento padrão. Projetado para fornecer 99,99% de durabilidade e 99,99 de disponibilidade. |

A AWS Garante para esse serviço:

- Durabilidade: 99.999999999% (arquivos não corrompidos e nem danificados)
- Disponibilidade: 99.95 a 99.99% (disponível em 99.99% do tempo ou disponível em 99.95 % do tempo)
- Tamanho mínimo de um arquivo = 1Byte
- Tamanho máximo para upload de arquivo = 5Tb
- Pode-se dividir o arquivo em partes para o upload e remontar tudo dentro do bucket.

#### Transfer Acceleration

O S3 Transfer Acceleration acelera as transferencias via internet entre o cliente e o bucket. O preço é baseado no local da borda da AWS usado para acelerar sua transferencia. A definição de preço do Transfer Acceleration é somado à definição de preço da transferência de dados.

 Classes de armazenamento S3:

| Classe                             | Descrição                                                    | Aplicação                                                    | Valor estimado(dolar)                                        | Redundância                   | Tipo de acesso                         |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------- | -------------------------------------- |
| S3 Standard                        | Alto nível de resiliência, disponibilidade e performance     | mídias utilizadas frequentemente por usuários;  Big Data - dados para análise em tempo real;<br />armazenar dados gerados pelo usuário em plataformas sociais | $0,023 a $0,021 por Gb                                       | sim                           | Imediato baixa lantência               |
| S3 Intelligent Tiering (IT)        | Alto nível de resiliência, disponibilidade e performance, serviço com inteligência para reduzir automaticamente o custo movendo os objetos para uma classe mais acessível caso não seja muito acessado. No nível de acesso frequente é otimizado. Custo até 40% menor que o Standard para os arquivos pouco acessados, 60% para os arquivos raramente acessados.<br />30 dias sem acesso -> Infrequent Access<br />90 dias sem acesso -> Archive Instant Access<br />180 dias ou mais -> Deep Archive Access | Backups que podem ser acessados de forma irregular (urgente ou não); Dados que podem ter acesso de forma irregular<br />Dados que podem ter picos de acesso<br />vídeos de alta resolução com acesso imprevistos | 0,0025 por 1000 objetos  acesso frequente ou $0,00099 por Gb objetos acesso raro | sim                           | Imediato de baixa latência             |
| S3 Express One Zone                | Alta performance, acesso de um milissegundo, aplicações sensível a alta latências. Até 50% mais barato que a Standard. Permite integração com o Sage Marker Model Training (IA de Machine Learn), Amazon Athenas  (IA de Machine Learn), Amazon EMR (IA de Machine Learn), e o AWS Glue (IA de melhoria da qualidade de dados)<br />Tem riscos de perda dos objetos uma vez que esta em uma única zona de disponibilidade | Cópias secundárias de backup; <br />Dados de log raramente acessados;<br />Dados de histórico de atendimento<br />Dados de projetos concluídos<br />Protótipos e versões antigas de software<br />Vídeos ou audios raramente acessados<br /> | $0,16 por Gb                                                 | Armazenado em apenas uma zona | Imediato de baixa latência             |
| S3 Standard IA(Infrequent Access)  | Armazenar dados de menor frequência de acesso, tem acesso rápido quando necessário.<br /> | Armazenar backups mensais ou anuais de sistemas e bases de dados que não são acessados regularmente;<br />Manter cópias de segurança de arquivos críticos;<br />Armazenar dados de transações financeiras ou registros de clientes que precisam ser retidos por um longo período;<br />Manter registros antigos de funcionários, folhas de pagamento, relatórios de desempenho e outros documentos relacionados a RH;<br />Manter cópias de materiais de marketing, publicações anteriores, vídeos de treinamento; | $0,0125 por Gb                                               | sim                           | Imediato de baixa latência             |
| S3 One Zone IA (Infrequent Access) | Baixa latência e voltado para arquivos de baixa frequência de acesso. Voltado para dados recriáveis. Até 20% mais acessível que o Standard IA | Cópias secundárias de backup; <br />Dados de log raramente acessados;<br />Dados de histórico de atendimento<br /> | $0,16 por Gb                                                 | Armazenado em apenas uma zona | Imediado baixa latência                |
| Glacier Instant Retrieval          | Custo baixo para objetos raramente acessados, exige recuperação com baixa latência 68% mais barato que o Standard IA | Arquivos médicos; Recursos de mídia; Noticias; Arquivos gerados pelo usuário; | $0,004 por Gb                                                | sim                           | Imediato de baixa latência             |
| Glacier Flexible Retrieval         | Baixo custo, 10% mais barato que o Glacier Instant Retrieval, arquivos acessados no máximo 2 vezes por ano e de forma assíncrona, flexibilidade para acessar grandes conjuntos de dados sem custo adicional.<br />Oferece criptografia para os objetos em repouso e SSL para objetos em transição | backup;                                                      | $0,0036 por Gb                                               | sim                           | configurável de minutos a horas        |
| Amazon S3 Glacier Deep Archive     | a mais acessível em questão de valores, armazenamento para preservação digital de longo prazo, acesso de 1 a 2 vezes ao ano, tempo de armazenamento de 7 a 10 ou mais anos. | Serviços financeiros; Saúde; Setor público;                  | $0,00099 por Gb                                              | sim                           | até 12 horas para recuperar os objetos |

  > valores podem sofrer alterações**

> [!TIP]
> Uso de Signed Url's com data de expiração pode ser uma solução para evitar que arquivos de imagens de seu bucket em sites de terceiros.

### Versioning - Versionamento no S3

Pode ser habilitado porém não pode ser desabilitado, uma vez acionado pode ser apenas pausado.

Gera uma nova cópia/versão do arquivo a cada modificação que for armazenada, ideal para casos onde a versão precisa ser armazenada, pode gerar maior custo do bucket pela quantidade de objetos armazenada.

Os objetos armazenados na S3 a partir do versionamento recebem um ID de versão exclusivo. Os que existiam recebem esse ID quando forem modificados por solicitações após a ativação do versionamento. Antes disso estes objetos estariam com ID nullo.

### Server Access Login S3

Armazena o histórico das ações dentro do bucket e quem as realizou, relatório de acesso. Gera custos adicionais.

### WebSite Estático no S3

Pode servir para armazenamento de páginas estáticas e sites HTML, tem URL única 

### CDN - content delivery S3

É um serviço de cache e entrega rápida para site estático que pode ser utilizado em conjunto com o S3 - **Cloud Front** quando se altera algo no site deve-se derrubar o cache e refazer para propagar a alteração. Atende em Zona local.

### Ciclo de vida S3 (life cycle)

Permite mover objetos do bucket de forma configurável e automática para customizar os custos do mesmo evitando guardar objetos desnecessários.

1. mover objetos atuais para classes de armazenamentos
2. mover objetos versão desatualizadas entre classes de armazenamento
3. expirar versões desatualizadas entre classes de armazenamento (exemplo as ultimas 5 versão permanece em uma classe as demais expirar)
4. excluir marcadores de exclusão de objetos expirados e carregamentos fracionados(documentos que são feitos quando o download da erro o bucket armazena no seu próprio bucket)

### Replicação de dados S3

> [!WARNING]
> É possível replicar um bucket para outra região para melhor atender outra filial da empresa por exemplo, para isso é necessário deixar habilitado o versionamento da bucket que se deseja replicar.

### Politica IAM S3

Cuidado com acesso público para buckets criados, aplicar regras de grupo, usuário, roles, escritas por json para listar, permitir e negar acessos.

> [!WARNING]
>Para a exclusão de arquivos no Bucket é possível adicionar uma etapa adicional de **MFA antes do objeto ser excluído**. Isso minimiza questões de **exclusão acidental**. Exclusão de MFA no bucket.


### Bucket Policy S3

Função por bucket, indicado para torna-lo mais seguro e definir regras de acesso

### Bucket ACL

ACL Lista de controle de acesso é um sub-recurso do S3 que permite o gerenciamento do acesso aos buckets e objetos. Esta lista define quais são os grupos ou contas da AWS tem acesso ao bucket e tipo de acesso. É definido no momento em que se cria o bucket. <u>Na documentação a AWS recomenda não habilitar a ACL, o proprietário do bucket possui todos os objetos do bucket e gerencia o acesso a eles exclusivamente usando políticas de gerenciamento</u>.

As ACLs são escritas em XML  e concedem todos os direitos ao dono do bucket.

### Criptografia S3

- **SSE-S3** - site server Encription - o S3 gerencia e define as chaves de criptografia - indicado
- **SSE-KMS** - quem gerencia as chaves de criptografia é o KMS, você define as chaves e salva a mesma no cofre(KMS) - indicado
- **SSE-C** - Cliente fornece as chaves e armazena no bucket - pouco indicado
- **CSE** - cliente fornece as chaves e armazena as mesmas fora do bucket - alto risco

### Segurança em S3 Modo Governança

Sistema de controle com flexibilidade para administradores, permite que usuário com esse perfil consigam alterar dados mesmo durante o período de contenção. Para ações onde se precisa de alto nível de proteção de dados mas ainda requer flexibilidade para os administradores.

### Segurança em S3 Modo Conformidade

É como um cofre inviolável, nem o usuário ADM consegue alterar algo até o período de contenção expirar. Ideal para atender requisitos regulatórios rigorosos onde os dados não podem ser modificados ou alterados antes de um tempo definido.

![Segurança em S3](./images/28.png)

 ![Governança e Conformidade S3](./images/29.png)

### Server Access Logging no S3

Recurso para conseguir visualizar dentro da bucket as ações, quem excluiu, alterou ... Seguindo-se os passos abaixo você ativa esse registro de logs e a partir dessa ação tudo que se for feito vai ficar um log no S3

1. Criar uma bucket de destino para os logs
2. Na bucket que se quer criar o log, em Propriedades 
3. Opção Registro em log de acesso ao servidor
4. Editar
5. Ativar
6. Selecione a Bucket destino
7. Salvar

### Habilitar bloqueio/permissão fora do IAM (policy)

Bucket policy é aplicado diretamente ao bucket e não ao usuário. 

- É escrita em Json e aplicada direto no bucket
- Pode ser utilizada para permitir/bloquear um usuário de acessa-la

```
{
	"Version":"2012-10-17",
	"Statement":[{
		"Sid":"Allow",
		"Effect":"Allow",
		"Principal":{
		"AWS":[
			"arn:aws:iam::6161616161:root",
			"arn:aws:iam::6161616161:user/jason"
		]
		},
		"Action":"s3:GetObject",
		"Resource":"arn:aws:s3:::foobucket/*"
	}]
}
```

#### ACL - List Access Control

Este seria o ultimo recurso a ser utilizado para filtrar o trafego (acesso) a um bucket. Lembre-se que esta é uma opção mais limitada e o melhor senário seria utilizar as Politicas aplicada ao bucket.

O proprietário da Bucket consegue por default Listar, Gravar, leitura e gravação.

#### Criar um role para conceder o acesso a uma S3 para um EC2

1. Dentro do IAM ir para o recurso Role/Função
2. Botão criar função
3. Opção Serviço da AWS, caso de uso EC2
4. Em politicas de permissão pesquisar por S3 e selecionar a opção: "AmazonS3FullAccess" ou "AmazonS3ReadOnly" dependendo da necessidade
5. De um nome para sua função e também uma descrição para ajudar a entender quem faz uso e qual o uso
6. Será gerado um Json com a role criada e suas permissões
7. Agora basta concluir.

## AWS Storage Gateway

Comunicação - dispositivo físico.

![Storage Gateway](./images/58.png)

- <u>Permite que os servidores da empresa consigam acessar um S3 ou outro Storage dentro da AWS.</u>
- Muito utilizado para backup.
- Tem sistema de cache

Pode ser aplicado de 3 formar:

1. File Gateway - utiliza o mesmo sistema de armazenamento do S3, é visto como um S3
2. Volume Gateway - Transporte de volumes
3. Backup Gateway - Backup de volumes

## Volume Efêmero

Volume efêmero fornece armazenamento temporário em nível de bloco para a instância EC2, esses discos são ideais para armazenamento temporário de dados alterados com frequência. É o tipo de disco padrão para alguns tipos de EC2.

## Armazenamento EBS Multi-atach (Elastic Block Store)

É um serviço de armazenamento em bloco da AWS. Ele oferece volumes de armazenamento persistente para instâncias do Amazon EC2, banco de dados(RDS). Armazenamento bruto em nível de bloco.

* até 16 instancias aceita apenas o Io1, instancias do tipo Nitro
* Dados continuam mesmo quando a EC2 é interrompida ou desligada.
* Você pode mudar a capacidade ou tipo de volume conforme necessário.
* Sempre da mesma AZ da EC2
* São replicados automaticamente dentro da zona de disponibilidade que estão.
* Move através do Snapshot
* Tipos de EBS:
  * SSD + rápido e + caro
  * HDD + lento e + barato (descontinuado)
* Uso Geral, volumes equilibrados adequados para uma ampla gama de workloads:
  * Tipo GP2 - SSD
  * Tipo GP3 - SSD
* Provisionado Iops, requerem alta performance como banco de dados
  * io1
  * io2
* Magnetic, opções de baixo custo para armazenamento de dados menos acessados.
  * sc1
  * st1
* Otimizado para taxa de transferência 
* Cold HDD - baixo custo - pouco acesso
* Snapshot - São cópias de um Snapshot que pode ser para outra região - utilizado tbm para backup

> [!TIP]
> Aplicação: **Hospedagem de websites**, **banco de dados**, **backup e recuperação de desastres**, execução de aplicações que requerem **baixa latência e alta IOPS**(input output operations per second)

## Coleta e processamento de dados - Amazon Kinesis Data Streams

Serviço serveless que coleta e processa dados em tempo real. Ideal para aplicações que exigem alta escalabilidade e baixa latência e processamento contínuo de dados.

Os dados conforme a demanda são divididos em shards, que são como malotes de dados que processar e armazenar os dados e isso permite que o serviço escale horizontamente para lidar com grandes volumes de dados em tempo real.

Casos de uso:

- Disney + usa o serviço para alimentar uma plataforma de vídeo acessada por milhões de clientes
- Comcast fornece tranmissão cde dados de alta performace com o Kinesis Data Streams
- Thomson Reuters usa Kenesis para construir uma pipeline de dados de transmissão para proporcionar insights mais rápidos e melhor experiência do usuário
- Hearst Corporation usa para uma solução centralizada de análise de sequência de cliques usando o Kinesis

Três camadas de serviços:

1. **Kinesis Data Streams** - coleta os dados em partes para processamento ou entrega em um destino ou outra sessão do Kinesis(pode reter dados 24 horas) ou **Kinesis Video Streams** que faz o mesmo papel do Data porém coletando vídeos.
2. **Kinesis Data Analitics** - análise de dados em SQL ele pode gravar esse dado posteriormente em um banco de dados DynamoDB por exemplo, ele faz a analise dos dados do Streams e do Firehose.
3. **Kinesis Data Firehose** - carrega os dados para um destino final como um bucket S3 - podendo utilizar um Athena para leitura/busca nesse S3 posteriormente(não retem dados)

![Amazon Kinesis Data Streams](./images/35.png)

![Amazon Kinesis Data Firehose](./images/36.png)

## Banco de dados

Banco de dados podem ser relacionais ou não relacionais. E cada um desses modelos tem como objetivo atender um determinado tipo de demanda.

### Amazon RDS

É um serviço que facilita a criação, operação e estabilidade de bancos de dados relacionais na nuvem. Permite que você escolha e configure facilmente um banco de dados relacional popular como MYSQL, PostgreSQL, Oracle, Sql Server entre outros sem necessidade de instalar ou gerenciar o software de banco de dados.  (**SaaS**) * * principal produto.

> [!TIP]
> O RDS cria um <u>certificado SSL</u> e instala o certificado na instância de banco de dados quando provisiona a instância. 
> Você pode fazer download de um certificado raiz da AWS que funcione para todas as regiões ou pode fazer download de certificados intermediários específicos da região e usar para conectar à instância de banco de dados RDS para garantir maior segurança.

![RDS](./images/40.png)

### Tipos de banco de dados:

#### Relacionais

* contem estrutura em linhas, colunas e campos/células
* multi AZ -> Desastre Recovery
* Read Replica -> cópia idêntica apenas para leitura (recurso para melhorar tempo de acesso/leitura aos dados)

#### Não Relacionais

* Flexível em adicionar ou remover informações/dados

### Elasticache

Não é um banco de dados tradicional, é um serviço de cache na memória que deve ser utilizado em conjunto com um banco de dados seja este relacional ou não relacional. É uma ferramenta agnóstica ao tipo de banco de dados e trás benefícios de desempenho e escalabilidade. Voltado para sistemas onde a escalabilidade e latência são críticos. 

* Aplicações de acesso rápido
* Não possui disco é em memória
* Utiliza In Memory Cache
* Memory Cache (utiliza objetos para armazenar)
* Opções de serviço:
  * **Redis**: banco de dados in memory mais popular oferece alta performance e flexibilidade - para dados quentes e com alta taxa de leitura
  * **Memcached**: Opção mais simples que o Redis, com menos funcionalidades

> [!TIP]
>  Aplicação: E-commerce para atender demandas altas como promoções ou feriados. Sistemas em tempo, como jogos online e sistemas de trading financeiro. Sessões de usuário e recomendações para usuários. Consultas complexas ou demoradas ao banco de dados.
> Não se aplica:  se o sistema tem baixo tráfego, sistemas que fazem muitas operações de escrita e poucas leituras exemplo: login. Sistemas com dados voláteis ou de curta duração. Sistemas onde a consistência dos dados é crítica, como sistemas bancários. 

![Elasticache](./images/41.png)

### Aurora

É um banco de dados que promete alta disponibilidade e rapidez dentro do modelo Relacional. Permite aumentar ou diminuir a capacidade da instância conforme necessário, com pouco ou nenhum tempo de inatividade.

* Multi -AZ
* AWS é proprietária
* Suporta transações complexas.
* Compatível com o o Mysql e PostgreSQL
* 5 x mais rápida que outros bancos
* 10 x mais barato
* já inicia com 10Gb e Auto Scaling Automático
* Uma base pode ter até 64Tb
* Data base principal
  * replicas : leitura até 15
  * latência baixa
  * recuperação point in time
  * backup continuo -> distribuído em 3 zonas -> pode ser feito em um bucket
  * alta disponibilidade de 99,99%

> [!TIP]
> Aplicação: Sistemas financeiros, ERP, CRM.
> Não se aplica: aplicações que podem ter esquema de dados não fixo, sistemas com alto nível de escrita no banco de dados pode ter um gargalo nesse operação. 

### DynamoDB

**Amazon DynamoDB** - banco de dados **não relacional**, **serveless** ou seja em nuvem e se paga pelo que é consumido e não pelas instancias adquiridas. É escalável (ilimitado em armazenamento e taxa de transferência ), confiável tem **backup continuo** dos últimos 35 dias. É rápido e tem latência em microssegundos.

* Multi -AZ

- Banco de dados não relacional, No Sql
- Mili segundos para acesso
- Aplicações de alto desempenho
- Key Value -> leitura de documentos
- Muito utilizado para games
- No mínimo 3 data centers
- Strongly Consistent Reads < 1 segundo
- SSD
- Pode escalar Horizontalmente automaticamente. 
- Atende muito bem Aplicações que tem necessidade de atender a mais de uma região, pois possui recursos como tabelas globais, que replica dados automaticamente entre regiões da AWS.
- *É possível usar esse serviço em conjunto com solução **Amazon SQS(Fila)**, **Amazon Auto Scaling** para tratar questões de tempo de processamento*

> [!TIP]
> Aplicação - Ecommerce, Games, Mobile ou IoT. Sistemas com consultas mais simplificadas e sem muitos dados binários.
> Não se aplica:  quando requer consultas complexas.
> OBS: o **Consistent Read** é i tempo delay entre a gravação do dado e a leitura do mesmo. Aqui temos o Strongly Consistent Reads que leva esse tempo de resposta para dados recém gravados para menos de 1 segundo.

### Redshift

É um serviço de banco de dados relacional, voltado para lidar com grandes volumes de dados e realizar consultas analíticas em grandes conjuntos de dados para relatórios,análises e insights.

* Multi -AZ
* Serviço de WareHouse(armazenagem)

* Ideal para executar consultas com Joins e processamento de grandes volumes de dados em tempo hábil.
* Pode-se escalar facilmente adicionar ou remover nós de cluster
* Compatível com o modelo de negocio BI. Fácil de integrar com aplicações de BI.
* Formado de colunas
* Dados com grande quantidade de itens (muitos dados)
* Compressão de dados
* Inicia com 160 Gb
* Single Node (uma instância)
* Compute Mode(!28 instâncias)
* Leitura em várias Databases MMP (Massive Paralel Processing)
* AWS pode gerenciar automaticamente as rotinas de backups, replicas e outros.

> [!TIP]
> Aplicação: Sistemas de BI (business intelligence), sistemas com consultas complexas, onde o volume de dados pode atingir Pentabytes.
> Não se aplica: aplicações que não atingem essa complexidade de dados, ou empresas de pequeno porte pode ser um custo não justificado. Exige uma boa estrutura de dados e planejamento(modelagem de dados). Sistemas de dados em tempo real.

## Serviços AWS

### Route 53

* Consegue dividir o trafego de DNS web definindo melhor servidor para entregar
* Roteia as querys DNS para servidores mais próximos no caso de se ter mais de uma instancia atendendo.
* Aplicação de políticas de geolocalização.
* Zonas Hospedadas: seu domínio no valor de 50centavos para os primeiros 25 domínios
* Dentro de zonas, criamos os registros A(sites) e MX(e-mail)
* Hosted Zones:
  * **Hosted zones públicas**: para sites e endereços públicos.
  * **Hosted zones privadas**: para conexões internas, como conexão com banco de dados, instancias onde se deseja usar um endpoint no lugar de ip do serviço.
* Politicas de roteamento:
  * **Simple Routing** - Roteamento simples - aplicação sites simples, com um único servidor ou aplicações onde todo o tráfego deve ser direcionado para um único recurso. *Desvantagens: se o recurso falhar o tráfego será perdido.*
  * **Weighted (ponderado)** - divide o trafego de chamadas no esquema um acesso para A, um acesso para B... também pode ser aplicado quando se deseja utilizar uma canary releases- pequena porção do trafego ser direcionado para uma nova versão da aplicação. *Desvantagens: necessita de monitoramento constante, se o recurso falhar o Route 53 não redireciona automaticamente*.
  * **Geo Location** - divide por localização, a requisição para para o host mais próximo. Aplicações que necessitam atender leis e dados regionais, oferta de serviços conforme a região. *Desvantagens: pode resultar em uma experiência inconsistente se a localização não for precisa, mais complexo de ser implementado.*
  * **Geo proximity** - mais especifico além de entregar a requisição para o host mais próximo avalia também o ajuste de preferência de roteamento para a localização específica. Aplicações que querem dar preferência a uma região específica, desejam controlar a quantidade de tráfego de cada região. *Desvantagens: requer mais gerenciamento e ajustes manuais para otimização, pode ser difícil prever como as alterações de proximidade afetarão a distribuição de tráfego.*
  * **Latência** - menor tempo de resposta, envia o usuário para o host de menor latência. Aplicações globais onde a experiência do usuário depende de baixa latência. Desvantagens: requer que os recursos estejam distribuídos geograficamente.
  * **Failover** - ativo-passivo verifica se o servidor pode atender se o mais próximo cair ele manda para ao próximo mais perto. Em outras palavras, permite que se defina um recurso primário e um para backup, se o primário falhar ele direciona o tráfego para o recurso de backup. Utilizar para aplicações que requer alta disponibilidade. *Desvantagens: depende da configuração e monitoramento adequado do health check. Se todos os tráfegos falharem, o tráfego será perdido.*

### CloudFront(CDN)

É um serviço AWS de rede de fornecimento de conteúdo CDN criado para alta performance. É um serviço global que distribui em proxy de servidores.

Estrutura de um conteúdo disponibilizado com CloudFront:

**Usuário** > Camada de **AWS Shield**(protege contra ataques DDos) e **AWS WAF**(firewall) > conforme a localização do usuário será direcionado para um **Edge Location** ou ponto de acesso de borda da AWS > acesso ao Cache com conteúdo > conteúdo que pode ser atualizado e que vem de uma **EC2** ou **S3** por exemplo.

Como podemos ver no fluxo acima o conteúdo não é armazenado em um CloudFront e sim conforme a demanda é feita apenas um cache do conteúdo o que torna o mesmo mais perto do usuário final e permite que o mesmo não sinta uma grande latência ao acessa-lo. Mas sempre que o conteúdo for atualizado, acessado pela primeira vez, será necessário resgata-lo do seu local de origem, seja esse loca um bucket S3 ou uma Instância EC2. Também poderíamos estar tratando aqui conteúdo vindo de um Gateway, Elastic Load Balancing, AWS Media Services, AWS Elemental ou de um servidor on-premises(local dentro de uma empresa privada).

* Responsável por diminuir latência.

* Replica nas Edges Locations o conteúdo em cache

* CloudFront Origins OAI(Origins Access Indentity) é o recurso que o CloudFront utiliza para acessar a origem do seu conteúdo de forma segura. Isso permite que apenas o CloudFront consiga acessar esse conteúdo em sua origem o usuário sempre vai precisar acessa-lo pelo CloudFront.

* Nome da URL vai conter o cloudfront.net

 > [!TIP]
 > **Permite aplicar restrição geográfica para bloquear acesso a países que por algum motivo não possa acessar um conteúdo distribuído com Cloudfront.**

![CloudFront](./images/37.png)


### Amazon SQS

Serviço para desacoplamento de aplicações redução de interdependência. Principais funções:

- criar filas de mensagens 
- desacoplamento de componentes
- é altamente escalável permite que processe grande volume de mensagens
- garante a entrega das mensagens
- se integra facilmente com outros serviços da AWS

![SQS serviço de fila de mensagens AWS](./images/34.png)

### AWS Elastic Beanstalk(Servless api)

- é um serviço que serve de tudo que é necessário para executar o seu aplicativo com segurança e eficiência na AWS, você só precisa levar o código do seu aplicativo e coloca-ló dentro desse ambiente. (**PaaS**)
- Quase que um plug and play para aplicativos

### AWS Fargate (Servless - container)

Serviço Server Less para containers permite executar container sem se preocupar com a infraestrutura subjacente, integrado com ECS e EKS ideal para desenvolvedores que querem focar no app containerizado focando só no app e não na estrutura.

### AWS API GATEWAY

-  Criar e gerenciar APIs para suas aplicações backend, permitindo que diferentes clientes (dispositivos móveis, aplicativos web, etc.) se conectem e consumam seus serviços

## Redes

Aprofundando nos conceitos de comunicação entre serviços e máquinas na AWS e com a AWS. 

### ENI

Interfaces de rede elástica (Elastic Network Interface)

Permite conectar uma instância com **subnets dentro da mesma zona de disponibilidade**. Não podemos conectar com outras zonas de disponibilidade ou região.

Esta rede pode vai ter ip privado e caso queira sair para internet um ip público também pode ser adicionado.

Suportado por todas as instâncias

![ENI](./images/17.png)

### ENA

Elastic Network Adapter é uma tecnologia mais atualizada em relação a ENI mas que oferece mesma solução com mais velocidade

Suportado por algumas instâncias

![ENA](./images/18.png)

### EFA

Elastic Fabric Adapter - é do tipo High Speed (altíssima velocidade) apropriada para Machine learning.

Suportado por algumas instâncias (P4d/P4de/DL1 são os tipos de instâncias permitidos)

<u>*Pode comunicar subnets em zonas de disponibilidade diferentes se aplicada em conjunto com o VPC Peering, lembrando que o VPC Peering pode adicionar uma maior latência nessa comunicação.*</u>

*<u>Se aplicada junto a Transit Gateway você pode conectar instâncias em múltiplos VPCs e zonas de disponibilidade com mais escalabilidade e gerencia.</u>*

![EFA](./images/19.png)

### NAT e Internet Gateway (IGW)

Network Address Translation - é o que vai garantir sua conexão com a internet é um mapeamento estático que pega o seu ip privado quando for sair para a internet receber o ip público. O internet Gateway consegue traduzir esse valor do endereço público para o privado.

![NAT](./images/42.png)

![Internet Gateway](./images/43.png)

###  Subnets privadas e públicas

Para as subnets privadas teremos instâncias que não precisam de acesso a internet e automaticamente não ficam acessíveis na internet. Isso pode ser a melhor opção para instâncias que precisam de nível a mais de segurança e não consomem ou não necessitam consumir nada na internet.

Para subnets públicas teremos o ip público e o acesso a internet.

Para toda essa estrutura teremos a tabela de roteamento trazendo o roteamento dos ips privados e públicos.

![Subnets pública x privada e Bastion Host](./images/44.png)

### Criar uma rede VPC

- **Amazon VPC** - serviço que permite criar rede privada virtual na nuvem e até mesmo sub-redes com tabelas de roteamento e regras de firewall. Essa rede é isolada do resto da internet e de outras redes da AWS. (**IaaS**)  | `Aplicação`: para **ter segurança aprimorada**, mantendo isolados e protegidos por acesso restrito alguns recursos - **Integração com ambiente local**, se a empresa já possui estrutura On-premise. - **Ambientes de teste**, para desenvolvedores ou equipe, podendo simular cenários sem afetar a infraestrutura. ** principal produto
- <u>OBS: podemos ter até 5 VPCs dentro de uma conta.</u>

#### Prática:

1.  Vá para o serviço VPC
2. Criar em Criar VPC
3. Dar um nome para sua VPC
4. Definir o seu bloco CIDR IPv4 - entrada manual de COPR IPv4 10.0.0.0/16
5. Para esse caso de estudo aplicar Nenhum bloco CIDR IPv6
6. Local = Padrão
7. Tags = VPC1 = nome da minha vpc
8. Botão criar VPC

![VPC criada com sucesso](./images/45.png)

#### Escolher zona de disponibilidade para essa VPC

1. Menu Subnets
2. Botão criar sub-redes(subnets)
3. Selecionar a VPC
4. Selecionar a Zona de Disponibilidade
5. Adicionar para o Bloco CIDR da subnet o valor ip, no caso será 10.0.1.0/24, 10.0.2.0/24 para a segunda, 10.0.3.0/24 e assim sucessivamente as seguintes. Criarei 4 subnets no exercício.
6. Botão Criar subnet

Resultado esperado:

![Subnets criadas com sucesso](./images/46.png)

#### Tornar subnets como pública

1. Selecionar a subrede
2. Menu ações - opção editar configurações de subrede
3. Habilitar endereço IPv4 de atribuição automática
4. Salvar

#### Tabela de roteamento

1. Ir até a opção tabela de roteamento do menu lateral
2. Atualizar as tabelas de roteamento e localizar a tabela associada a sua VPC criada(imagem abaixo)
3. Vamos criar mais uma tabela de roteamento para ter uma apontando as subnets públicas para internet e a outra comunicação apenas interna.
4. Vamos renomear a tabela de roteamento para internet como -public sendo o prefixo conforme sua preferência. (imagem abaixo)
5. Clicar no botão Criar tabela de rotas
6. Adicionar nome a tabela de roteamento
7. Selecionar a VPC que estamos trabalhando
8. Botão Criar tabela de rotas

![Tabela de roteamento](./images/47.png)

![Tabela de roteamento](./images/48.png)

#### Adicionar subnets nas tabelas de roteamento

1. No painel das Tabelas de Roteamento clique na tabela de roteamento pública
2. Ir até a guia Associações de sub-rede
3. Botão Editar associações de sub-rede
4. Selecionar as subredes que atribuímos o IPv4 automático
5. Clicar no botão Salvar associações

OBS: para esse exercício vamos aplicar a tabela de roteamento privada para as outras duas sub-redes em um processo igual ao que fizemos anteriormente.

#### Internet Gateway - acesso a internet

1. Ir para opção Gateways Internet no menu lateral
2. Criar Gateway da Internet
3. Dar nome ao seu gateway
4. Botão Criar gateway da internet

#### Ligar Tabela de roteamento ao Gateway Internet para ter conexão na internet

1. Ainda na tela do Gateway que criamos ir no botão Ações
2. Opção Associar a VPC
3. Selecionar o VPC que criamos
4. Botão Associar Gateway da Internet
5. Volte na tela de Tabelas de roteamento e selecione a tabela -public que foi criada
6. Ir na Guia Rotas
7. Botão Editar rotas
8. Botão Adicionar rotas
9. Em IP deixar 0.0.0.0/0
10. Selecionar o Gateway de internet que criamos
11. Botão Salvar alterações

 ![Associar a tabela de roteamento com a internet gateway e nossa VPC](C:\Users\tijac\Documents\aws\estudo\images\49.png)

#### Criar uma EC2 na subnet pública e na subnet privada

1. Buscar pelo serviço EC2
2. Executar instâncias
3. Dar um nome para a instância
4. Sistema Operacional Linux
5. Tipo T2.Micro
6. Chave - criar uma novo ou usar uma que já tiver
7. Em configuração de rede clicar em Editar
8. Informar em VPC a VPC que criamos
9. Selecionar a Subnet conforme criamos também, no caso vou inserir ela em uma subnet pública
10. Atribuir IP público automaticamente vamos habilitar
11. Habilitar Grupo de segurança
12. Nomear o Grupo de segurança
13. Por ser um ambiente de teste e aprendizado vamos deixar liberado em Regras do Grupo de segurança o tipo como Todo o tráfego
14. Botão Executar Instância

#### Testar a internet dentro da instância

1. Selecionar a instância
2. Clicar em Conectar 
3. Selecionar Conectar-se usando o EC2 Instance Connect
4. Botão conectar
5. executar o comando `ping google.com`

Resultado esperado:

![Ping de dentro de uma instância para internet](./images/50.png)

> [!TIP]
> Você pode tentar criar as demais instâncias, sendo pelo menos uma para cada subnet.
>Após criar as instâncias você também pode testar a conectividade pingando no ip de cada uma das máquinas. 

#### Bastion Host

Antes de realizar o Bastion Host na prática vamos entender oque temos acesso e o que não temos:

> [!WARNING]
>
> - Ao tentar acessar a máquina privada no power shell do console aws ele não consegue conectar pois não temos um ip público
> - Ao tentar acessar essa máquina pelo ip privado realizando um ping a partir de uma das instâncias públicas vamos ter êxito
> - Ao tentar acessar essa máquina pelo ssh a partir de uma das instâncias públicas vamos ter um retorno que de a autenticação do host não pode estabelecer conexão pois precisamos passar a chave da máquina.
> - A mensagem a seguir é um erro de conexão que vamos trabalhar a seguir.

![Tentando acessar a instância privada a partir de uma instância pública com SSH](./images/51.PNG)

1. Abrir a sua chave da instância privada que vai ser acessada e copiar seu conteúdo completo
2. Na sua instância pública deve realizar a conexão no power shell do console da AWS
3. Criar um arquivo com mesmo nome que sua chave já tinha comando: `nano nome da sua chave.pem`
4. No editor deve-se colar o  código da chave que foi copiada
5. Pressionar Ctrl + o para sair da digitação do documento e salvar
6. Pressionar Ctrl + x para sair do arquivo
7. Ainda na tela do Power Shell dentro da console da AWS vamos realizar alguns comandos, mas para isso volte na sua instância privada, clicar em Conectar, depois vá até Cliente SSH, você deve copiar a linha de comando `chmod 400 "nome da sua chave.pem"`
8. O código copiado deve ser colado no Power Shell onde estamos conectados com a instância pública
9. Enter
10. Copie novamente da instância privada a linha de comando que vai fazer a conexão agora e também execute em sua instância pública `ssh -i "sua chave.pem" ec2-user@seu ip privado`
11. Confirme com yes

![Conexão realizada na instância privada a partir da instância pública](./images/52.png)

> [!TIP]
> Agora já estamos conectados a máquina privada a partir da instância que estava pública, tudo que a gente realizar vai ter como destino a máquina privada e para voltar a operar na instância pública basta sair com comando `exit`

#### Como rodar atualizações em instâncias privadas?

Para permitir que as máquinas privadas consigam sair para internet e atualizar sem ficar exposta na internet vamos criar um Nat Gateway.

##### Criar um Nat Gateway

1. Menu lateral do VPC opção Nat Gateway
2. Botão Criar Gateway NAT
3. De um nome para seu Nat Gateway
4. Selecionar o subnet da instância privada que vamos aplicar a saída para internet (apenas saída)
5. Opção de conectividade pode deixar público
6. Botão Alocar IP Elástico
7. Botão criar Gateway NAT

Agora vamos definir na Tabela de Roteamento que essa instância privada tem uma rota para sair para internet

Conferir se já temos acesso a internet, a partir da instância public no Power Shell

1. Linha de comando `sudo su`
2. Passar a instrução de qual a máquina queremos utilizar agora `ssh -i "chave.pem" ec2-user@ip da maquina`
3. Tentar pingar em um site público qualquer para ver se tem saída para internet
4. Vamos então entrar no serviço de roteamento, tabela de roteamento
5. Botão editar na tabela de roteamento privada
6. Botão Adicionar Rota
7. Preencher com o ip 0.0.0.0/0
8. Informar a opção Gateway NAT
9. Selecionar o Gateway NAT que criamos no passo anterior
10. Salvar Alterações
11. Você pode refazer os testes de conectividade para a instância privada e ela deve pingar no site público, reiniciar a instância caso necessário

### Conexões entre VPCs 

Para conectar poucas VPCs entre sí temos uma solução que seria o pareamento entre VPCs **Peering Connect**, mas quando temos muitas VPCs esse tipo de conexão não é tão assertivo devido ao trabalho envolvido. 

Podemos ter então um **Transit Gateway**. (conexão entre VPCs para muitas VPCs)

Para conectar suas VPCs e seu On-Premise podemos ter uma **Full Mesh**.

Prática:

1. Criar duas VPCs, podendo ser cada uma em uma Região, para essa parte criei uma VPC em Oregon e uma em Virginia
2. Estando em uma dessas duas regiões no seu console da AWS, vamos no serviço VPC recurso Peering Connections
3. Botão Create Peering Connection
4. Adicionar nome da VPC(opcional)
5. Em VPC ID escolher a sua VPC local, aquela que você criou para esse exercício
6. Escolher se a segunda VPC esta dentro da sua conta ou fora, caso esteja fora deve-se informar o ID da conta
7. Escolher esta VPC esta na mesma região ou outra região, vamos selecionar outra região e informar a região (imagem abaixo)
8. Botão Create Connection...
9. Vamos agora para o painel da segunda VPC, aquela que recebe o pedido de conexão, para aceitar a mesma. (imagem abaixo)
10. Você pode confirmar se é a nossa requisição e aceitar a requisição(imagem)
11. Vamos validar a comunicação entre as VPCs pingando de uma maquina pública de um VPC em uma máquina pública da segunda VPC 
![Informando região e VPC id da VPC que foi criada na segunda região](./images/54.png)

![Mensagem de sucesso ao requisitar a conexão](./images/55.png)

![A requisição vista da VPC que recebe o pedido de conexão](./images/56.png)

![Aceitar a requisição de conexão entre VPCs Peering](./images/57.png)



### VPN ( AWS x On Premises)

![VPN](./images/26.png)

- Aplicação para interligar redes de VPC diferentes como On Premise com AWS
- Simples de configurar e gerenciar 
- Ideal para pequenas e médias empresas
- <u>Desvantagem: pode apresentar latência e limitação de banda especialmente para grandes volumes de dados</u>

### Direct Connetc  ( AWS x On Premises)

- Estabelece conexão dedicada de alta velocidade entre rede local e on Premise. 
- Baixa latência, maior banda e maior segurança em comparação a VPN
- <u>Desvantagem: requer investimento inicial</u>

### AWS Site-to-site   ( AWS x On Premises)

-  Pode ser aplicado <u>junto com o Direct Connect combinando as vantagens de ambas as tecnologias</u> e entregar de tráfego crítico
- Pode ser aplicado <u>com a VPN para tráfego de menor prioridade</u>.
- <u>Desvantagens: complexidade da configuração.</u>

### AWS Transit Gateway  ( AWS x On Premises)

- Permite conectar múltiplas CPCs e redes on-premises em uma única rede, simplificando a gestão de conectividade
- Escalabilidade e flexibilidade para grandes redes
- <u>Desvantagens: Pode ser mais complexo de configurar e gerenciar</u>

### AWS OutPost ( AWS x On Premises)

- Estende os serviços AWS para seu data center, permitindo executar workloads(conjunto de recursos computacionais e aplicações que trabalham juntos) na AWS localmente.
- Ideal para workloads com requisitos de baixa latência e alta segurança
- Desvantagens: requer investimento inicial significativo

### AWS Global Accelerator

Serviço de rede que ajuda a melhorar a disponibilidade, performance e segurança de aplicações públicas. Ele tem dois ips fixos que sevem de entrada para os endpoints de suas APIS funciona como o Load Balancer só que atendendo APIS.

## Segurança

### AWS Directory Service

É um serviço que permite atribuir funções do IAM aos usuário e grupos do AWS Manage Microsoft Ad ou Simple Ad na nuvem. Se dentro da sua empresa você já tem um Microsoft AD, você pode usar este na AWS.

### Identity Federation 

- Autenticação de redes sociais para acesso ao IAM
- É uma forma de utilizar autenticação externa para permitir conectar ao IAM

### Cognito

Serviço de autenticação da AWS, pode ser feita a autenticação em um sistema(desenvolvido pela sua empresa) utilizando o facebook ou outra plataforma similar ele tem duas partes:

- **User pool** -> diz se o usuário informou um usuário e senha correto, ou se logou pelo facebook com sucesso
- **Identity pool** -> diz a que conteúdos o usuário pode acessar após logado.

### Encryption

Tipos de encryption:

1. **In Transit** - criptografia para dados em trânsito. SSL, HTTPS
2. **At Rest** - criptografia para dados em repouso, ou que já estão armazenados
3. **Simétrico** - a chave aplicada para realizar a criptografia é a **mesma chave** que desfaz a criptografia o dado.
4. **Assimétrico** - a chave aplicada para realizar a criptografia **é diferente da chave** que desfaz a criptografia o dado.

### Key Manager Service (KMS)

Chaves de criptografia que são gerenciadas pela AWS, ele trata essa chave atualizando a mesma quando necessária conforme definido.

É um serviço compartilhado esta disponível para todos os clientes AWS

### Cloud HSM

É um serviço muito parecido com o KMS, sua diferença é que ele é dedicado, esta em um hardware dedicado para sua empresa. AWS não consegue visualizar as chaves.

## IA na AWS

### Amazon Rekognition

Serviço da AWS que consegue varrer imagens e identificar nesta imagem: Pessoas, Texto, Objetos.

É muito utilizado para: Moderação de chats e outros ambientes, identificar placas de carros, identificar faces.

### Amazon Transcribe

IA que converte Fala em texto(utiliza ASR e entende em diversas línguas, possui PII ou seja oculta informações pessoais como CPF, RG...). Pode ser associado a serviços de telefonia e outros transcrevendo o que esta sendo conversado.

O serviço de PII você pode configurar quais dados vc quer que ele ignore, oculte. Exemplo ele vai marcando a transcrição os dados que estiverem habilitados para ser ocultos por tags [numeroCPF] ou [numeroCartãoCredito].

### Amazon Polly

Faz a leitura de um texto, você pode escolher o idioma da leitura, tipo de leitura Neural(mais natural) ou Padrão que é uma fala um pouco mais robótica. Também é possível escolher a voz que faz a leitura e também baixar o áudio em formato mp3.

### Amazon Translate

É utilizado para tradução de websites e outros documentos, podem escolher o idioma origem e o idioma de saída. 

Para texto é possível apenas digitar, também é possível enviar um documento para ser traduzido.

### Amazon Lex

Sistema de linguagem que é o utilizado pela Alexa, utiliza ASR para converter tudo que é solicitado para texto e utiliza NLU para pesquisar na internet a sua resposta, é utilizado para chatbot e call center.

### Amazon Sagemaker

É utilizado por cientistas de dados para criar Machine learn e IA, é possível criar uma nova linguagem ou uma nova IA com este serviço.

1. Rotular os dados
2. Construir - transformar os dados em blocos de anotações
3. Treinar - usar algoritmos estruturas para treinamento distribuído
4. Ajustar - o Sagemaker ajusta automaticamente seu modelo.
5. Implementar
6. Descobrir

### Amazon Kendra

Você conectar ao Kendra S3, SharePoint, Salesforce, Onedrive, Google drive, banco de dados... esse serviço vai ler os documentos e banco de dados e vai conseguir extrair essas informações para por exemplo responder em um site perguntas dos usuários.

### Amazon Textract

Você passa uma imagem para ele, e ele consegui ver os textos de uma imagem e extrair esse texto para um arquivo txt.

### Amazon Macie

Serviço da AWS para privacidade e segurança de dados, ele pode examinar um documento atrás de PII.(dados privados como CFP, número de cartão de crédito/ debito)

## Outros serviços AWS

### Amazon AppFlow

Consegue enviar dados de uma plataforma (Slack, Salesforce, Zendesk) para um destino de sua preferencia, exemplo de destinos: S3, Redshift. Google Analytics ou Salesforce. Essa transmissão dos dados da origem para o destino será feito de maneira encriptada podendo gerar filtros dessas mensagens.

### AWS Batch

Processamento em lote, utilizado para ML e análise em lote. Cada Batch job tem a sua definição (diz o que deve ser feito), e tem a fila onde os dados serão executados. Após executar  ele vai armazenar tudo que foi apreendido da análise desses dados em um Storage.

### AWS Amplify

Para criar aplicações Mobile, ele cuida da autenticação do seu app, cria api para falar com outras aplicações, permite conectar seu codigo ao Github, permite conectar com as IAS da AWS, permite monitoramento da app.

### Amazon Cost Anamaly Detection

Verifica qualquer anormalidade da área de custos da sua empresa. Precisa ser feita a configuração dele para poder receber esse apoio. Ele evita surpresas de uma escalada de valores pois ele vai usar IA para verificar e acompanhar seus custos baseado no seu próprio consumo dentro da AWS, qual sua média de custos e quais os serviços que você costuma utilizar.

Formar de monitoramento:

1. serviços
2. contas de membros da AWS
3. tags
4. categorias de serviços

Esse serviço consegue guardar um histórico de anomalias, monitores de serviços por tags...

### AWS System Manager Patch Manager 

É um serviço AWS Patch Manager tem um recurso AWS System Manager para automatizar o processo de aplicação de patches aos nós gerenciados com atualizações relativas a segurança e atualizações.

## Aws Lambda

- permite executar código sem a necessidade de provisional ou gerenciar servidores, é como um assistente que executa pequenos trechos de código (funções) em resposta a eventos específicos. ( exemplo de eventos: solicitação http, upload de um arquivo no bucket ou alteração em um banco de dados) (**PaaS**)

## Redes e entrega de conteúdo

- **Amazon Route 53** - serviço de DNS fornecido pela AWS que permite conectar nomes de domínio a recursos na internet.  Também oferece outros recursos úteis, como o registro de recursos de  saúde dos servidores, para garantir a alta disponibilidade dos recursos  da web, e o balanceamento de carga, que distribui o tráfego entre vários servidores para melhorar o desempenho. (**SaaS**)
- **Amazon CloudFront** - Serviço de entrega de conteúdo, acelera a entrega na web de vídeos, imagens e arquivos de página web - através de um cache e aceleração ele consegue entregar o arquivo a partir do ponto de presença mais próximo, ele ajuda a proteger o conteúdo contra ataques DDoS e outros tipos de ameaça.  Faz uso de LOCAIS de BORDA e CACHE para tratar latência. (**SaaS**)
- **Elastic Load Balancing** - Serviço que ajuda a distribuir o tráfego de rede de forma eficiente entre vários servidores ou instâncias em uma aplicação. Balanceamento de carga a solicitação de acesso a uma url vai passar por ele primeiro, Distribuição de tráfego ele distribui os acessos entre as instâncias ativas para atender o serviço e ajuda a evitar que um único servidor fique sobrecarregado, alta disponibilidade pois esta sempre acompanhando a saúde dos servidores, Elasticidade pois ele vai se adaptando automaticamente as mudanças acionando os servidores adicionais ou pausando esses conforme demanda. (**SaaS**)
  - Application Load Balancer(ALB) é o Elastic Load Balancer baseado na camada 7 do modelo OSI - aplicação então ele consegue ver o path do endereço e direcionar conforme o mesmo para o destino correto, pode ser também direcionado conforme o subdomínio do site. ROTEAMENTO MAIS DETALHADO
  - Network Load Balancer(NLB) é baseado na camada 4 do modelo OSI - aplicado ao endereçamento IP, então consegue trabalhar. ROTEAMENTO MAIS RÁPIDO

### Gerenciamento e Governança

- **Amazon CloudWatch** - Um serviço da AWS que permite monitorar recursos e aplicações em nuvem em tempo real, ele coleta e rastreia métricas, logs e eventos importante que ocorrem nos serviços da AWS.  (**SaaS**) ** principal produto
- AWS Auto Scaling
- AWS Truted Advisor
- **AWS Organizations** - organiza a parte financeira da sua AWS, permite gerenciar e controlar seu ambiente de maneira centralizada. Serviço global gerencia todas as contas da AWS, centraliza o faturamento, faz junção de custos e gera economia com pooling de instancias reservadas. Possui camada de segurança colocando restrições nas contas com SCP.
- **AWS Cloud Formation** - é um serviço que oferece uma linguagem comum para que você possa descrever e fornecer todos os recursos de infraestrutura em um ambiente de nuvem. permite que você utilize um arquivo de texto para modelar um ambiente em nuvem (json ou Yaml por exemplo). Paga pelos recursos que configurou e não pelo Cloud formation. É uma forma de trabalho que ajuda a manter uma organização na estruturação da sua nuvem, ele oferece formas de acesso (AWS `Command Line Interface`, `Gerenciador de console AWS` ou `SDKs`) onde vc escolher um template (modelo pra gerar uma estrutura ) ou criar sua própria template - que vai gerar sua Stack (que é uma pilha de comandos para gerar suas instancias e configurações), **permite replicar uma configuração em nuvem várias vezes e ter um gerenciamento de versões e alterações**.
- **AWS Config** - Responsável por gerenciar mudanças, auxilia nas auditorias, compliance. Permite acessar, auditar e avaliar as configurações dos recursos da AWS. Restrito a uma região, configura-se regras(checklist). Notificação por Amazon SMS caso tenha sido contratado, armazena os dados em um bucket S3. 
- **AWS CloudTrail** - é um serviço que possibilita a governança, conformidade, auditoria operacional e auditoria de riscos em sua conta AWS, **diferença entre ele e o CloudWatch é que o CloudWatch tem foco em desempenho e o CloudTrail é conformidade e auditoria** (**trilha de como foi feito e quem quando e tudo em log**). Podemos criar uma trilha para acompanhar alguma ação ou ainda no Dashboard teremos uma visão geral, ele mantem 90 dias de histórico e pode-se criar a trilha para acompanhar por mais de 90 dias. Ideal para acompanhar que alterou ou deletou algum serviço.

### Segurança, identidade e compliance:

- **AWS Identity & Access Management** - é um serviço que ajuda você a controlar e gerenciar o acesso aos recursos da sua conta na AWS, o IAM funciona como um "porteiro ele permite que seja feita as configurações para conceder ou negar permissões para usuários, grupos e até mesmo outros serviços da AWS. ** principal produto (**SaaS**)
- **AWS WAF** - é um f**irewall de aplicativos web** que permite especificar quais tráfego tem o seu acesso permitido ou bloqueado, mediante a regras pré-definidas e personalizáveis. Filtro por endereço Ip, por cabeçalhos, pelo corpo http e alguma strings uri, bloquear requisições maliciosas com **SQL injection** ou **Cross-site Scripting**, **bloquear por países**, size constraints (tamanho da requisição) e rate base-rules
- **AWS Shield** **Standard** - proteger o ambiente **contra ataque D-Dos** ( distributed Denial of Service) - varias requisições simultânea para matar a aplicação ou deixar lento o servidor. Serviço grátis.
- **AWS Shield Advanced** - você contrata o serviço com uma equipe para suporte 24x7 que investem contra esse tipo de ataque esse serviço é pago. oferece proteção extra no **Amazon EC2**, **Elastic Load Balancing**, **Amazon CloudFront**, **AWS Global Accelerator** e o **Route 53**.
- **AWS Artifact** - acordos e relatórios de conformidade. aqui encontramos AICPA SOC, ISO 27001, FedRAMP, irap, pci, nist, HIPAA, C5 e outros. 

### Gerenciamento de custos:

- **Calculadoras AWS** - é uma ferramenta gratuita que estima os custos dos serviços da AWS que você planeja utilizar. (**Saas**)
- **AWS Cost** - ferramenta de **análise de custos** que faz parte da AWS Management Console, exibe custos detalhados por conta. São custos já ocorridos. (**SaaS**) Aqui conseguimos ver serviço, conta vinculada, região...
- **AWS Budgets ou Orçamentos** - Ferramenta que permite que você defina limites de gastos personalizados para os seus recursos. Também é possível **criar alerta para esses valores limite definidos**. (**SaaS**)

- 

## Escalabilidade e elasticidade 

**Escalabilidade** diz respeito ao serviço que é escalável, ou seja, pode crescer de acordo com as necessidades para atender. Exige uma constante observação do comportamento da requisição. Ver se limites são ultrapassados com qual frequência e em que momentos. Assim podemos definir:

- número mínimo de instancias;
- número desejado de instancias;
- número disponível para escalonar de instancias
- número máximo de instancias;

Sendo o máximo o número mínimo mais o número disponível (ou seja o total de recursos que se tem a disposição). 

> Escalabilidade   =  **Amazon EC2 Auto Scaling**

Benefícios do Auto Scaling:

1. Melhorar a disponibilidade
2. Obter um ambiente tolerante a falhas - se uma instancia cair outra assume
3. Refletir nos custos operacionais

**Elasticidade** conseguir aumentar um recurso computacionais, mas sempre poder voltar ao número menor depois.

> Exemplos dessa elasticidade estão nos serviços: **Amazon EC2**, **Elastic Load Balancing**, **AWS Elastic Beanstalk** e **Amazon Elastic Cache**.

- **Escalabilidade** - aumentar/ diminuir número de instancias - servidores
- **Elasticidade** - aumentar/ diminuir recursos computacionais(memória, armazenamento...)



## Serviços Globais e Regionais

**Serviços regionais**:

A maioria dos serviços são regionais, ou seja, se você iniciar esse serviço em uma região ele esta em um data center, se você alterar a região ele vai deixar de estar disponível naquela região.

- EC2
- AWS Lambda
- AWS Elastic Beanstalk
- Amazon EC2 Auto Scaling

**Serviços Globais**:

Serviços globais independem de uma região, você pode configurar e depois acessar de qualquer região.

- Amazon CloudFront
- Amazon Route 53
- AWS Identity & Access Management
- AWS Waf

## Planos de suporte

- **Basic** - Grátis, é oferecido a todos os clientes da AWS, tem suporte limitado, não permite abrir tickets. Acesso ao AWS Trusted Advisor (serviço de recomendação e orientação para otimizar o ambiente de nuvem) 7 itens, inclui acesso a documentação, fóruns, recursos de auto atendimento. Ideal para uso em ambientes de desenvolvimento e testes com baixas exigências de suporte.
- **Developer** - Oferece acesso ao suporte técnico por e-mail durante horário comercial. Ajuda resolver questões técnicas e problemas relacionados a serviços AWS, indicado para desenvolvedores que precisam de um pouco mais de suporte para ambientes de produção de menor escala. Custo de $29,00, nível experimentação. Acesso ao AWS Trusted Advisor (serviço de recomendação e orientação para otimizar o ambiente de nuvem) 7 itens. Abrir tickets apenas 1 pessoa. SLA até 24 horas horário comercial.
- **Business** - suporte 24x7 com tempos de resposta rápido(até 1 hora) e suporte aprimorado. Inclui um gerente de sucesso do cliente dedicado para fornecer orientação estratégica(um terceirizado). Ideal para empresas que necessitam de um suporte completo e personalizado para ambientes de produção críticos. Ticket com mais de uma pessoa, suporte por e-mail, telefone e chat, acesso completo ao  AWS Trusted Advisor (serviço de recomendação e orientação para otimizar o ambiente de nuvem), custo de $100,00, ambiente de produção.
- **Enterprise on-Ramp** - custo de $5.500,00 . acesso completo ao  AWS Trusted Advisor (serviço de recomendação e orientação para otimizar o ambiente de nuvem), suporte por telefone, e-mail e chat 24x7, ticket para mais de uma pessoa, SLA de 30min para sistema critico inativo, orientações de interoperabilidade suporte por terceiros e concierge e orientação arquitetura.
- **Enterprise** - custo de $15.000,00, para operações de missão crítica, acesso completo ao  AWS Trusted Advisor (serviço de recomendação e orientação para otimizar o ambiente de nuvem),  suporte por telefone, e-mail e chat 24x7, ticket para mais de uma pessoa, SLA de 15min para sistema critico inativo, orientações de interoperabilidade suporte por terceiros e concierge e orientação arquitetura e TAM.

Dicas para prova: 

- plano que precisa de suporte técnico, elimine o basic
- plano com até 1 hora para suporte técnico SLA - o mais barato é o business
- apenas o enterprise tem suporte técnico Tam e Concierge que ajuda a baixar os custos

## Nível gratuito AWS

A AWS oferece alguns serviços grátis, mas ainda é necessário inserir seu cartão de credito para ter uma conta na AWS, isso porque se sua ações dentro desse ambiente utilizar de recursos pagos você será cobrado. 

Tipos de oferta:

- sempre gratuito:  não expiram e estão disponíveis para todos os clientes AWS, porém tem limite de uso que se for ultrapassado gera cobranças.
- 12 meses Gratuitos: é ofertado grátis dentro do prazo de 12 meses e após isso se torna pago, a contar da data de seu cadastro inicial na AWS.
- Testes: ofertas de teste gratuito de curto prazo começam na data em que você ativa determinado serviço.

Sobre o nível gratuito: https://aws.amazon.com/pt/free/

## AWS Trusted Advisor 

Afinal o que é o AWS Trusted Advisor? É um recurso oferecido pela AWS visando o melhor aproveitamento dos serviços pensando em alguns pilares:

- ​	Otimizar os custos com dicas/alertas com indicações de melhor ajuste dentro da nuvem. (aqui teremos visão de serviços subutilizados, instancias de banco de dados ociosas, endereço ip estático não associado, tempo limite excessivos em funções lambda ...)
- Performance melhorada dos serviços em uso levando em consideração configuração x uso(uso de computação EC2 e configuração no Cloudfront ou taxa de transferência e latência)
- Segurança melhorada sugerindo práticas recomendadas básicas de segurança, Chaves de acesso expostas, permissões desnecessárias do bucket S3.
- Tolerância a falhas para melhorar a confiabilidade de seus serviços, (grupo EC2 auto scaling, verificações de integridade excluídas no Route 53, zonas de disponibilidade desabilitadas e backups de RDS desabilitados)
- Cotas de serviço- são os números máximo de recursos que você pode criar em uma conta, podemos ser notificados quando atingir 80% de uma cota de serviço.

## AWS IQ

Recebe ajuda sob demanda de especialistas terceirizados e certificados. É uma forma mais facil de encontrar profissionais certificados e qualificados para soluções de demanda específica em sua nuvem; Você pode confiar e ter a colaboração segura, entregando chaves de acesso e caso necessário você pode remover o acesso do profissional a qualquer momento; Pagamento integrado, ou seja, pagar dentro da sua conta AWS o especialista terceirizado.

## AWS Skill Builder

Espaço de aprendizado da AWS.

Possui 3 planos:

- **Gratuito**: mais de 600 cursos sob demanda e planos de aprendizado ; cursos preparatórios para exames padrão; conjunto de perguntas oficiais da AWS Certification; AWS Cloud Quest: Cloud Practitioner; Crachás Digitais
- **Assinatura individual**: todo plano grátis + Acesso ilimitado a mais de 1225 laboratórios; Cursos aprimorados de preparação para exames; AWS Cloud Quest - funções intermediárias e avançadas; AWS Industry Quest; Exames simulados oficinas da AWS Certification; Jornada AWS Jam;
- **Assinatura de equipe**: Tudo do plano individual e mais Capacidade de atribuir treinamento individual e em equipe; painel administrativo; relatórios abrangentes; eventos do AWS Jam; Logon único (opcional)

3. 

## Well-Architected

É o uso de boas práticas na nuvem. Tornando o ambiente mais seguro e econômico.

### Princípios gerais:

- parar de adivinhar a sua capacidade
- testar o produto em escala de produção
- automatizar a arquitetura para uma experimentação fácil
- permita a evolução na arquitetura
- construir a arquitetura baseado em dados - uso de ferramentas de monitoria para isso
- Melhorar através de gamedays - testes de eventos do mundo real para ver como o sistema se comporta - esta ante falhar e redundantes diante de momentos de caos
  - escalabilidade vertical e horizontal
  - recursos descartáveis nada é para sempre
  - automação: serveless IaaS auto scaling
  - Loose couple: falhar não podem cascatear não ao monólito
  - serviços não servidores: será que não tem um serviço para isso?

### 5 pilares Well-architected

1. **operational excellence**: executar e monitorar para entregar valor
2. **security**: proteger informações e sistemas
3. **reliability**: garantir que uma carga de trabalho execute sua função pretendida corretamente e de modo consistente
4. **performance efficiency**: uso eficiente de recursos e computação
5. **cost Optimization**: compreensão e controle de onde o dinheiro esta sendo gasto, ajustando os recursos e serviços

## AWS Budgets - orçamento de serviços

É um serviço que permite definir limites de gastos e receber alertas quando os custos da sua conta atingirem determinado valor. É possível criar limites mensal ou escolher uma meta personalizada, se os custos ultrapassarem esse limite, a AWS enviará um alerta para notificar por e-mail e por meio de notificação na AWs management Console.

### Como criar um alerta:

1. Pesquisar pelo serviço na busca do portal AWS
2. clicar em criar um orçamento 
3. opção Personalizado - Avançado 
4. orçamento de custos final da página - botão próximo 
5. preencher nome do orçamento
6. escolher opção período mensal 
7. orçamento recorrente repete todo mês 
8. Mês que vamos iniciar Junho 
9. orçamento corrigido custo = U$1,00(dólares)
10. Todos os serviços 
11. custos não combinados 
12. botão Próximo 
13. adicionar alerta
14. botão criar orçamento

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095608794394747/image.png)

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095642193625248/image.png)

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095698275680278/image.png)

![resultado esperado](https://cdn.discordapp.com/attachments/1123729724812841021/1124095862843396096/image.png)

## AWS Cost Explorer

Monta gráficos para avaliar o uso de serviços, tem uma interface fácil de usar que permite visualizar, entender e gerenciar os custos e o uso da AWS ao longo do tempo.

Dica:

**Para gerar relatório de qual serviço esta gerando maior custo, ou qual região utilizar o serviço AWS Cost Explorer, lá é possível tbm gerar arquivo CSV com os dados.**

O **AWS Cost Explorer oferece interface para visualizar entender e gerenciar os custos** e o uso da AWS ao longo do tempo, já a **AWS Budgets é para definir orçamento(quanto espero gastar)** e enviar alertas quando o uso excede o valor orçado.

![AWS Cost Explorer](https://cdn.discordapp.com/attachments/1123729724812841021/1124096036063940738/image.png)

> DICA para prova: 
>
> - **Cost explorer** - você acompanha histórico do que já gastou, análise de histórico de gastos
>
> - **Budgest** -  se manter dentro de um orçamento, alerta de quando o orçamento estiver chegando ao limite
> - **calculadora** - previsão de gastos futuros, estimativas.
> - **AWS Config** - auxiliar em auditorias, é regional, mantem histórico de ações e alterações de configurações dos serviços AWS
> - **AWS Organizations** - serviço global permite gerenciar múltiplas contas - tem api para criação de contas, permite incluir restrições as contas.
> - **AWS Artifact** - documentos(artefatos), relatórios (ISO, PCI, SOC), atende a auditorias internas e conformidades 
> - **AWS CloudTrail** - governança, conformidade auditoria de riscos - trilha de quem fez, quando tudo em logs
> - **Amazon CloudWatsh** - monitorar recursos e aplicações em tempo real.
> - **IAM** -  gerencia acesso aos recursos, é como um porteiro.
> - **AWS CoudFormation** - você pode por meio de arquivo json ou Yaml configurações de permissões e ou serviços da AWS



## Calculadora de preços da AWS

É o serviço que ajuda ter uma prévia/ estimativa dos serviços antes de implementa-lós em sua conta AWS, é um simulador de custos para nuvem. Link:https://calculator.aws/#/ 

## AWS CLI

É uma forma de interagir com os serviços da AWS por linha de código que pode agilizar o desenvolvimento quando se precisa atender altas demandas com tarefas parecidas, evitando seguir um caminho de cliques.

## SDK Software Development Kit

São os kits de desenvolvimento para as tecnologias dentro do ambiente AWS, para atender demandas com Javascript, Go, .Net entre outras.

## Serviço AWS budgets - prática

1. clicar em criar um orçamento 
2. opção Personalizado - Avançado 
3. orçamento de custos 
4. final da pagina - botão próximo 
5. preencher seu nome 
6. escolher opção período mensal 
7. orçamento recorrente repete todo mês 
8. Mês que vamos iniciar Junho 
9. orçamento corrigido 
10. custo = valor que se deseja ter como limite 
11. Todos os serviços 
12. custos não combinados 
13. botão Próximo 
14. adicionar alerta
15. botão criar orçamento

Prints:

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095608794394747/image.png)

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095642193625248/image.png)

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095698275680278/image.png)

Resultado esperado:

![img](https://cdn.discordapp.com/attachments/1123729724812841021/1124095698275680278/image.png)

> 

## WAF - dicas

- WAF é um Firewall de aplicações web
- Atua na camada 7 -> HTTP
- Bloqueia SQL Injection (SQLi) e Cross-site scripting (XSS)
- Geo-match (bloqueio países), size constraints(limitar tamanho das requisições) e rate based-rules(limitar quantidade, requisições por segundo)

## AWS Config - dicas

- Aws Config é regional
- auxilia na auditoria das alterações dos recursos para compliance
- mantém histórico das alterações e armazena em um bucket s3 para posterior análise
- notificações de alterações são enviadas com o Amazon SNS e disponibilizadas na Dashboard painel do AWS Config
- não faz parte do plano free tier.

## AWS Organization - dicas

- é um serviço global
- permite gerenciar multiplas contas
- uma conta principal - master account
- api disponível para criação de contas
- restrição das contas usando SCP - service control police

## AWS Artifact - dicas

- Os documentos são chamados de artefatos
- os relatórios de segurança e compliance são ISO, PCI e SOC
- Os acordos de uso de serviços(agreements) são BAA e HIPAA
- são utilizados em auditorias internas e conformidade

## AWS CloudTrail -prática

1. procurar pelo serviço na caixa de pesquisa
2. clicar no botão Create Trail
3. dar um nome para a trail
4. ao criar a trail ele vai gerar um bucket s3, ele vai sugerir um nome para esse bucket, mas pode-se usar um existente, para laboratório vamos deixar ele criar
5. Events - event type  opção Management events - para ter visibilidade a eventos de chamada de API, criação de instancias, buckets| Data events são atividades de invocação de funções lambdas, get, put, delete | insights events ele analisa os volumes de chamadas para os recursos e te oferece insights - laboratório vamos marcar apenas o primeiro mesmo
6. clicar botão proximo
7. clicar em create trail
8. ele cria um bucket e o trail, ele leva uns 15 min
9. após isso lembre-se de deletar o trail para não gerar custos - apague tbm o bucket (esvaziar o mesmo primeiro)

## CloudFront prática **em desenvolvimento

- Criar uma distribuição
- definir o bucket
- opção cros

## RDS - prática

1. pesquisar pelo serviço RDS
2. verifique que não tem nenhuma instancia sendo executada 
3. clicar em `Create Data Base`
4. escolher a opção de método de criação - deixar o método Standard create (padrão)
5. escolher a engine option (mecanismo) - vamos optar pela opção Mysql
6. escolher a versão do Mysql - conversar com o cliente sempre para escolher a melhor versão 
7. **templates** escolher a opção Free tier
8. **Settings** vamos colocar o nome da instancia  no campo DB Instance Identifier 
9. em credenciais de acesso - podemos alterar o nome do usuário, mas por padrão é a Admin
10. criar a senha ou clicar em gerar uma senha, você pode escolher a opção mais viável
11. na opção **Burstable classes includes t classes** - ele não vai trazer nenhuma instancia pq estamos na opção Free tier para escolher uma instancia clique no botão "include previous generation classes", agora uma das instancias ficara disponível a menor  seria a `db.t2.micro`(vamos usar essa como treino)
12. **Storage Type** - vamos manter o `General Purpose` - tipo de disco pode ser configurado tbm conforme a necessidade
13. em **Storage autoscaling** - podemos definir se nosso tamanho de disco pode ser escalado (aumentado) conforme a demanda, e qual o tamanho máximo ele pode escalar, como se trata de um teste vamos desmarcar a opção `Enable storage` Autoscalling.
14. em **Availabillity e durability**, podemos definir o **Multi-AZ deployment** para permitir que esse banco seja replicado em outras zonas de disponibilidade caso um servidor caia outro venha a assumir por exemplo ou eliminar latência durante um backup. na versão Free Tier não temos como habilitar essa opção
15. **Connectivity/ conectividade** - vamos escolher aqui uma VPC que é sua rede privada na nuvem, essa VPC não deve ser alterada depois que o banco subir. Por isso escolhemos a nossa região e onde estão nossos clientes antes de criar o banco.
16. configurando backup - em **backup retention period** podemos definir o período de retenção de backup, exemplo os dados ficarem retidos em backup 30 dias...  para o laboratório vamos desmarcar a opção de backup automático para evitar cobranças.
17. **Monitoring** - monitorar ajuda a identificar melhorias no banco de dados - vamos deixar desmarcado para efeito de laboratório 
18. **manutenção** - ajuda a ter uma janela onde se poderá parar o banco e realizar manutenções - não vamos alterar o padrão
19. **Deletion Protection** - aqui é possível proteger o banco contra deleção, para laboratório não marcar essa opção.
20. no final da página teremos o resumo, leia confirme e clique no botão para gerar o banco de dados.
21. Caso tenha escolhido a opção de gerar a senha de acesso ao banco automaticamente, agora vc vai ver no topo da página um botão onde terá essa informação. Botão `View credential details` guarde suas informações em lugar seguro.
22. atualize a página para ver o status do banco atualizado. Aguarde até ele iniciar uma instancia.
23. Se você criou apenas para laboratório é indicado apagar o mesmo ao final. Mas antes observe se a opção Create final Snapshot esta marcada, ela indica que será feita uma cópia do banco antes de apagar e isso pode gerar custos então desmarcar essa opção.
24. Marque a caixa onde confirmamos que temos certeza que vamos continuar com a deleção e vamos sim perder as opções de backup ou copias automáticas do banco.
25. vamos digitar delete me na caixa de texto para confirmar a deleção.
26. clicar em deletar.

## Amazon DynamoDB

## AWS GuardDuty

Serviço AWS que monitora sua conta AWS em tempo real buscando acessos anônimos ou atividades suspeitas. Utiliza-se de Inteligência Artificial.

## AWS Inspector

Serviço da AWS que trabalha monitorando sua instancia em busca de não conformidades de segurança ou melhores práticas. Esta ligado ao princípio de conformidade, auditor de segurança. Identificar vulnerabilidades em instâncias.



## Dicionário AWS

| Termo       | Definição                                                    |
| ----------- | ------------------------------------------------------------ |
|             |                                                              |
| Compliance  | Estar de acordo com as regras/leis de um estado, pais, empresa. Adaptação dos serviços a região e empresa a qual se atende, seguindo as regras e leis vigentes. |
| On Premises | Servidores locais, muitas vezes instalados no local onde o a empresa esta operando. Aqui a empresa tem que as responsabilidades de manter toda parte física e lógica em funcionamento e com as suas devidas atualizações. |

