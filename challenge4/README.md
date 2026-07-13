<<<<<<< HEAD
# O que é o AWS CloudFormation

O **AWS CloudFormation** é um serviço da Amazon Web Services (AWS) que permite criar e gerenciar infraestrutura na nuvem utilizando código, em vez de configurar recursos manualmente pelo console da AWS.

## Como funciona

No CloudFormation, a infraestrutura é definida em um **template**, escrito em **YAML** ou **JSON**. Esse template descreve todos os recursos que devem ser criados, como:

- Instâncias EC2
- Buckets S3
- Bancos de dados RDS
- Redes VPC
- Funções IAM
- Load Balancers

Após enviar o template, o CloudFormation cria e configura automaticamente todos os recursos na ordem correta.

## Principais vantagens

- **Infraestrutura como Código (IaC):** permite versionar a infraestrutura junto com o código da aplicação.
- **Automação:** reduz tarefas manuais e erros de configuração.
- **Reprodutibilidade:** facilita a criação de ambientes idênticos (desenvolvimento, homologação e produção).
- **Gerenciamento centralizado:** atualiza e remove recursos de forma controlada.

## Conceitos importantes

### Template
Arquivo que define a infraestrutura.

### Stack
Conjunto de recursos criados a partir de um template.

### Change Set
Permite visualizar quais alterações serão realizadas antes de atualizar uma stack.

## Exemplo simples de template

```yaml
AWSTemplateFormatVersion: '2010-09-09'

Resources:
  MeuBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-exemplo
```

Este exemplo cria um bucket do Amazon S3 chamado `meu-bucket-exemplo`.

## Quando utilizar

O AWS CloudFormation é recomendado quando se deseja:

- Automatizar a criação de infraestrutura.
- Padronizar ambientes.
- Controlar mudanças utilizando versionamento.
- Facilitar implantações repetitivas.
- Implementar práticas de DevOps e Infraestrutura como Código (IaC).

## Resumo

O AWS CloudFormation é uma ferramenta de **Infraestrutura como Código (IaC)** que permite definir recursos da AWS em arquivos de configuração. Com isso, é possível criar, atualizar e excluir ambientes de forma automatizada, consistente e segura, tornando o gerenciamento da infraestrutura mais eficiente.