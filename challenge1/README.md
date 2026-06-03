# Introdução aos serviços AWS: EC2, EBS, Lambda e S3

Este documento fornece uma visão geral prática e concisa sobre quatro serviços fundamentais da AWS: **EC2**, **EBS**, **Lambda** e **S3**. Destina-se a desenvolvedores e operadores que querem entender quando usar cada serviço, boas práticas, exemplos rápidos com AWS CLI e pontos de custo/segurança.

---

## Amazon EC2 (Elastic Compute Cloud)

- **O que é:** Serviço de máquinas virtuais na nuvem (instâncias) configuráveis por tipo, CPU, memória e rede.
- **Quando usar:** Aplicações que precisam de controle total do sistema operacional, cargas persistentes, containers sem orquestrador gerenciado, bancos de dados não gerenciados ou workloads legadas.
- **Exemplo rápido (criar instância t2.micro):**

```bash
aws ec2 run-instances --image-id ami-0abcdef1234567890 --instance-type t2.micro \
  --key-name MinhaChave --security-group-ids sg-0123456789abcdef0 --subnet-id subnet-01234567
```

- **Boas práticas:**
  - Use AMIs oficiais e mantenha imagens atualizadas.
  - Automatize com CloudFormation/terraform.
  - Habilite Auto Scaling para disponibilidade.
  - Separe instâncias por função e use tags para gerenciamento.

---

## Amazon EBS (Elastic Block Store)

- **O que é:** Volumes de bloco persistentes usados como discos para instâncias EC2. Podem ser criptografados e dimensionados.
- **Quando usar:** Armazenamento persistente ligado a instâncias EC2 para sistemas de arquivos, bancos de dados e logs que requerem IOPS previsíveis.
- **Exemplo rápido (criar volume gp3 de 20 GiB):**

```bash
aws ec2 create-volume --availability-zone us-east-1a --size 20 --volume-type gp3
```

- **Boas práticas:**
  - Escolha o tipo de volume conforme IOPS/throughput (gp3, gp2, io2).
  - Faça snapshots regulares e automatize com Lifecycle policies.
  - Use criptografia (EBS encryption) para dados sensíveis.

---

## AWS Lambda

- **O que é:** Serviço de Functions-as-a-Service (FaaS) que executa código em resposta a eventos, sem gerenciar servidores.
- **Quando usar:** Workloads com execução esparsa, eventos por HTTP (API Gateway), processamentos assíncronos (SQS, SNS), ETL leves, integrações ou automações.
- **Exemplo rápido (implementar função Node.js via ZIP):**

```bash
aws lambda create-function --function-name minhaFuncao \
  --runtime nodejs18.x --handler index.handler --zip-file fileb://func.zip \
  --role arn:aws:iam::123456789012:role/minhaRole
```

- **Boas práticas:**
  - Mantenha funções pequenas e com responsabilidade única.
  - Use environment variables e parâmetros no AWS Systems Manager (SSM) ou Secrets Manager.
  - Controle de versão e aliases para deploy seguro.
  - Observe limites de tempo/recursos e faça testes de cold start se latência for crítica.

---

## Amazon S3 (Simple Storage Service)

- **O que é:** Armazenamento de objetos altamente disponível e escalável para arquivos, backups, assets estáticos e dados de big data.
- **Quando usar:** Armazenamento de objetos, hospedagem de sites estáticos, backups, logs, datasets e integração com serviços como CloudFront e Athena.
- **Exemplo rápido (fazer upload de um arquivo):**

```bash
aws s3 cp arquivo.txt s3://meu-bucket/pasta/arquivo.txt
```

- **Boas práticas:**
  - Habilite versioning para proteção contra sobrescrita/exclusão acidental.
  - Use políticas de ciclo de vida para mover objetos entre classes (Standard → Intelligent‑Tiering → Glacier).
  - Configure políticas de bucket e políticas IAM granulares.
  - Habilite criptografia em repouso (SSE-S3, SSE-KMS) e criptografia em trânsito (HTTPS).

---

## Segurança e IAM

- Princípio do menor privilégio com políticas IAM.
- Use roles para serviços (ex.: Lambda assume role com permissões mínimas).
- Habilite logging (CloudTrail) e monitoramento (CloudWatch, GuardDuty).

## Custos e otimização

- **EC2/EBS:** cobrado por horas/segundos de instância e por GB e IOPS do EBS; reserve instâncias ou use Savings Plans para reduzir custo.
- **Lambda:** cobrado por número de execuções e duração (GB‑segundo); otimizar memória e tempo reduz custos.
- **S3:** cobrado por armazenamento, requests e transferência de dados; usar classes de armazenamento e lifecycle.

## Links úteis

- Documentação EC2: https://docs.aws.amazon.com/ec2/
- Documentação EBS: https://docs.aws.amazon.com/ebs/
- Documentação Lambda: https://docs.aws.amazon.com/lambda/
- Documentação S3: https://docs.aws.amazon.com/s3/

---

## Próximos passos sugeridos

- Adicionar exemplos com Terraform/CloudFormation para cada serviço.
- Incluir fluxos de CI/CD para deploy de Lambdas e AMIs.

---

Arquivo gerado em: README.md
