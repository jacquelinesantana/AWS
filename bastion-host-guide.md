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
