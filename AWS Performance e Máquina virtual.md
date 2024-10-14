# AWS Performance e Máquina virtual

## Elastic Load Balancer

Este é um serviço AWS que permite distribuir o trafego de rede para aprimorar a escalabilidade da aplicação. Pode ser aplicado em EC2 com auto Scaling , AWS Lambda, Fargate, EKS, ECS.

Possui 3 tipos de Balanceadores:

### Aplication Load Balancer 

 Aplicado a casos de: roteamento baseado em conteúdo, saúde dos servidores(health checks), sticky sessions e Algoritmos de balanceamento de carga.

Atende baseado em HTTP Headers, para casos onde precisam de roteamento baseado no conteúdo da requisição como Lojas virtuais, blogs.

### Gateway Load Balancer

Aplicado a casos de: camada 4 TDP/IDP, isolamento de zonas, sticky sessions e conexões TCP de longa duração. Este serviço esta para ser descontinuado pela AWS.

### Network Load Balancer

Aplicado a casos de: Isolamentos de zonas, Verificar saúde dos servidores(health checks), sticky sessions, conecções TCP de longa duração.

Tráfego TCP e UDP como jogos online, streaming de vídeos e alta performance.

Questões de prova para ALB e NLB:

- Aplicativo atras de um NLB e o NLB não esta detectando erros HTTP para o aplicativo -> Substituir o NLB por ALB e habilitar verificações de integridade de HTTP fornecendo a URL do aplicativo, configurar a ação de auto scaling para substituir as instâncias com falhas.