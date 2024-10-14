# AWS Segurança

## AWS Secrets Manager

Serviço que gerencia o ciclo de vida de chaves de criptografia de maneira centralizada. Aplica-se para chaves de bancos de dados de api, estabelece de forma automatizada a rotação de chaves para atender requisitos de segurança e conformidade, pode ser aplicado em conjunto com o Lambda para proporcionar a rotatividade das chaves.

### Questões de prova do AWS Secrets Manager

- Rotaciona as credenciais dos bancos de dados regularmente e automaticamente -> O AWS Secrets Manager armazena as credenciais de banco de dados, pode-se ativar a rotação automática para a credencial, anexando a permissão necessária ao papel do EC2(ou serviço que requer ver a credencial) para conceder acesso ao segredo.
- 





## AWS Firewall Manager

Ferramenta para centralizar as regras de firewall em todas as suas contas AWS. Então com esta ferramenta você facilita o trabalho quando esta lidando com múltiplas contas e com o **AWS Organizations**. 

Ele vai atuar junto a outros serviços AWS tais como o **AWS WAF** que é um firewall da AWS e também com o **AWS Network Firewall**, outros serviços que estaram atuando aqui são os: **AWS Shield**, **Amazon Route 53 Resolver DNS Firewall**, **Security groups**, **Third-party Firewall**.

### Questões de prova sobre o Firewall Manager:

Solução contra ataques de Injeção de SQL e scripts para uma API Gateway -> Configurar o AWS Firewall Manager e centralizar as regras do WAF.

## AWS Certificate Manager ACM

Serviço para provisionar e gerenciar certificados SSL/TLS com serviços AWS e recursos conectados.

### Questões de prova para o ACM

- ELB usa certificados que são importados para o AWS Certificate Manager, a equipe de segurança deve ser notificada 30 dias antes da expiração de cada certificado -> Criar uma regra do AWS Config que verifica certificados que expiram dentro de 30 dias, configurar o Amazon EventBridge(Amazon CloudWatch Events) para invocar um alerta personalizado por meio do SNS quando o AWS Config relatar um recurso não conforme.

