# Guia de Implementação de Bastion Host na AWS

## Introdução
O Bastion Host (também conhecido como Jump Server) é um servidor especial que serve como ponto de entrada para acessar instâncias em uma rede privada de forma segura. Ele atua como uma ponte entre a internet pública e seus recursos privados.

## Arquitetura
- VPC Pública: Onde ficará o Bastion Host
- VPC Privada: Onde ficarão as instâncias de aplicação
- NAT Gateway: Para permitir que instâncias privadas acessem a internet
- Security Groups e NACLs: Para controle de acesso

## Passo a Passo

### 1. Criação da VPC
1. Acesse o Console AWS > VPC > Create VPC
2. Configure:
   - Nome: MyProjectVPC
   - CIDR: 10.0.0.0/16
   - Tenancy: Default
   

**Por que?** O CIDR 10.0.0.0/16 oferece um range de IPs privados suficiente para nosso ambiente.

### 2. Criação das Subnets
1. Crie a subnet pública:
   - Nome: Public-Subnet
   - CIDR: 10.0.1.0/24
   - AZ: us-east-1a
   - Auto-assign public IP: Yes

2. Crie a subnet privada:
   - Nome: Private-Subnet
   - CIDR: 10.0.2.0/24
   - AZ: us-east-1a
   - Auto-assign public IP: No

**Por que?** Separamos em subnets públicas e privadas para isolamento de recursos.

### 3. Internet Gateway
1. Crie um Internet Gateway
2. Anexe à VPC criada

**Por que?** Necessário para permitir comunicação com a internet.

### 4. NAT Gateway
1. Crie um NAT Gateway na subnet pública
2. Aloque um Elastic IP para ele

**Por que?** Permite que instâncias na subnet privada acessem a internet para updates.

### 5. Tabelas de Roteamento
1. Para a subnet pública:
   - Destino: 0.0.0.0/0
   - Target: Internet Gateway

2. Para a subnet privada:
   - Destino: 0.0.0.0/0
   - Target: NAT Gateway

**Por que?** Define como o tráfego será roteado dentro da VPC.

### 6. Security Groups

1. Bastion Host SG:
```
Inbound:
- SSH (22): Seu IP/32
Outbound:
- All Traffic: 0.0.0.0/0
```

2. Private Instance SG:
```
Inbound:
- SSH (22): Bastion Host SG
Outbound:
- All Traffic: 0.0.0.0/0
```

**Por que?** Security Groups são stateful e controlam o acesso no nível da instância.

### 7. Network ACLs
1. Subnet Pública:
```
Inbound:
- 22 (SSH): Seu IP/32
- 1024-65535 (Ephemeral): 0.0.0.0/0
Outbound:
- All Traffic: 0.0.0.0/0
```

2. Subnet Privada:
```
Inbound:
- 22 (SSH): 10.0.1.0/24
- 1024-65535 (Ephemeral): 0.0.0.0/0
Outbound:
- All Traffic: 0.0.0.0/0
```

**Por que?** NACLs são stateless e fornecem uma camada adicional de segurança no nível da subnet.

### 8. Criação das Instâncias

1. Bastion Host:
```
- AMI: Amazon Linux 2
- Tipo: t2.micro
- Subnet: Pública
- Security Group: Bastion Host SG
- Key pair: Criar novo
```

2. Instância Privada:
```
- AMI: Amazon Linux 2
- Tipo: t2.micro
- Subnet: Privada
- Security Group: Private Instance SG
- Key pair: Mesmo do Bastion
```

### 9. Testando o Acesso

1. Conecte ao Bastion Host:
```bash
ssh -i key.pem ec2-user@bastion-ip
```

2. Do Bastion Host, conecte à instância privada:
```bash
ssh -i key.pem ec2-user@private-instance-ip
```

3. Teste a conexão internet na instância privada:
```bash
sudo yum update
ping google.com
```

## Considerações de Segurança
- Mantenha o Bastion Host atualizado
- Use MFA quando possível
- Monitore os logs de acesso
- Considere usar AWS Systems Manager Session Manager como alternativa ao Bastion Host
- Implemente rotação regular de chaves
- Habilite CloudTrail para auditoria

## Boas Práticas
1. Use diferentes key pairs para Bastion e instâncias privadas em produção
2. Implemente auto-scaling para o Bastion Host em ambientes críticos
3. Configure backup e recuperação de desastres
4. Implemente monitoramento e alertas
5. Documente todos os processos e procedimentos

# Prática
## Criar a instância com acesso a internet
1. Criar a VPC
2. Criar um Internet Gateway e atachar com a VCP que vc criou
3. Criar uma tabela de roteamento com saída para o internet Gateway e uma local
![resultado esperado sua rota com as indicações de saída para a subnet](https://github.com/user-attachments/assets/6181bdb5-7f33-4977-a2c0-80eb041fa15f)
5. Criar a subrede pública com as seguintes configurações:
     1. vincular a rota criado a esta subrede
     2. definir o numero máximo de máquinas que podem se conectar a esta subrede com o CIDR IPV4 pode ser um /20 ou /24
     3. ative o auto-assign public IPv4 address
![resultado esperado confira se o vcp e tabela de roteamento são as que você criou](https://github.com/user-attachments/assets/73d6bf76-b156-4d4c-9bbf-20b0be5eb43d)
6. Criar um grupo de segurança com as seguintes configurações:
     1. adicione um acesso para seu ip para porta 22 acesso SSH
![Inbound exemplo](https://github.com/user-attachments/assets/bb54a651-f7bb-4607-bf2f-e0de1f1383c9)
![outbound exemplo](https://github.com/user-attachments/assets/6dddd5f1-9ad2-461c-9991-4b1de0202625)
7. Criar uma instância com as seguintes configurações:
     1. edite as configurações de VPC e informe a sua VPC
     2. informe a subnet publica que foi criada
     3. informe o grupo de segurança criado anteriormente com acesso via SSH seu ip liberado
![Resultado esperado, confirme se os pontos marcados estão com as informações da sua VPC, sua subrede...](https://github.com/user-attachments/assets/7dea0ad0-4e14-4ee9-b91e-6524505c4098)
Podemos fazer um teste acessando essa instância e tentando realizar ping em algum site.
## criar a instância com acesso privado
1. Criar uma tabela de roteamento sem acesso a Internet Gateway
![resultado esperado: Tabela de roteamento](https://github.com/user-attachments/assets/663b79df-3441-4754-b5fc-c6246e1e409d)
2. criar a subnet e relacionar ela a sua tabela de relacionamento sem internet Gateway
![resultado esperado: confirme se o subnet esta configurada com sua VPC e sua tabela de roteamento](https://github.com/user-attachments/assets/6f868760-a489-4a6a-a46a-a8d963748fa8)
3.  Criar um grupo de segurança que de acesso ao bastion host da seguinte forma:
      1. 
5. 
