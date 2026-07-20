# Automação de Tarefas com AWS Lambda e Amazon S3

## Introdução

A combinação entre **AWS Lambda** e **Amazon S3** permite criar soluções automatizadas sem a necessidade de gerenciar servidores. Sempre que um evento ocorre em um bucket S3, uma função Lambda pode ser acionada automaticamente para processar arquivos, gerar relatórios, enviar notificações, entre outras tarefas.

Essa arquitetura faz parte do modelo **Serverless**, no qual a infraestrutura é totalmente gerenciada pela AWS.

---

# Arquitetura

```text
                Upload de Arquivo
                       │
                       ▼
              Amazon S3 (Bucket)
                       │
                Evento (PUT, DELETE...)
                       │
                       ▼
                AWS Lambda Function
                       │
       ┌───────────────┼────────────────┐
       ▼               ▼                ▼
 Processa arquivo   Envia e-mail   Salva em Banco
```

---

# O que é Amazon S3?

O **Amazon Simple Storage Service (S3)** é um serviço de armazenamento de objetos altamente escalável.

Principais características:

- Armazenamento ilimitado
- Alta disponibilidade
- Versionamento
- Criptografia
- Eventos automáticos
- Integração com diversos serviços AWS

Exemplos de uso:

- Backup
- Upload de imagens
- Hospedagem de arquivos
- Data Lake
- Armazenamento de logs

---

# O que é AWS Lambda?

AWS Lambda é um serviço de computação Serverless que executa código sob demanda.

Características:

- Não precisa criar servidores
- Escalabilidade automática
- Pagamento por execução
- Suporte a diversas linguagens:
  - Python
  - Node.js
  - Java
  - C#
  - Go
  - Ruby

---

# Como funciona a automação

Fluxo:

1. Um usuário envia um arquivo para um bucket S3.
2. O S3 gera um evento.
3. O evento aciona uma função Lambda.
4. A Lambda executa alguma ação automaticamente.

Exemplos:

- Redimensionar imagens
- Converter arquivos CSV
- Gerar PDFs
- Validar documentos
- Processar vídeos
- Criar miniaturas
- Atualizar banco de dados
- Enviar notificações

---

# Eventos do Amazon S3

Os principais eventos são:

| Evento | Descrição |
|---------|-----------|
| ObjectCreated | Novo arquivo enviado |
| ObjectRemoved | Arquivo removido |
| ObjectRestore | Arquivo restaurado |
| Replication | Replicação concluída |
| Lifecycle | Mudança por política de ciclo de vida |

Exemplo:

```text
Upload de foto.jpg

↓

Evento:
ObjectCreated:Put

↓

Lambda é executada
```

---

# Exemplo em Python

```python
import json

def lambda_handler(event, context):

    bucket = event['Records'][0]['s3']['bucket']['name']
    arquivo = event['Records'][0]['s3']['object']['key']

    print(f"Bucket: {bucket}")
    print(f"Arquivo: {arquivo}")

    return {
        'statusCode': 200,
        'body': json.dumps('Arquivo processado!')
    }
```

---

# Casos de Uso

## 1. Redimensionamento de imagens

Upload:

```
foto.png
```

↓

Lambda

↓

Gera

```
foto_thumbnail.png
```

---

## 2. Conversão de arquivos

Upload:

```
clientes.csv
```

↓

Lambda

↓

Converte para

```
clientes.json
```

---

## 3. Envio automático de e-mails

Upload de contrato PDF

↓

Lambda

↓

Amazon SES

↓

Cliente recebe confirmação.

---

## 4. Processamento de Logs

Aplicações gravam logs no S3.

↓

Lambda analisa

↓

CloudWatch

↓

Alarmes são enviados.

---

## 5. Extração de dados

Upload de XML

↓

Lambda

↓

Extrai informações

↓

Banco de dados

---

# Configurando um gatilho (Trigger)

1. Criar um bucket S3.
2. Criar uma função Lambda.
3. Conceder permissões via IAM.
4. Configurar o evento do bucket.
5. Fazer upload de um arquivo para testar.

---

# Permissões IAM

A função Lambda deve possuir permissões para acessar o bucket S3.

Exemplo de política:

```json
{
    "Version":"2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource":"arn:aws:s3:::meu-bucket/*"
        }
    ]
}
```

---

# Vantagens

- Arquitetura Serverless
- Escalabilidade automática
- Baixo custo
- Alta disponibilidade
- Fácil integração
- Execução sob demanda
- Sem gerenciamento de servidores

---

# Limitações

- Tempo máximo de execução da Lambda.
- Dependência de permissões IAM corretas.
- Limites de memória e armazenamento temporário.
- Eventos simultâneos podem exigir controle de concorrência.

---

# Boas Práticas

- Utilizar o princípio do menor privilégio nas políticas IAM.
- Registrar logs no Amazon CloudWatch.
- Tratar exceções e erros.
- Validar arquivos antes do processamento.
- Monitorar métricas e custos.
- Versionar o código da função Lambda.
- Utilizar variáveis de ambiente para configurações.

---

# Exemplo de Fluxo Completo

```text
Usuário
   │
   ▼
Upload de imagem
   │
   ▼
Amazon S3
   │
Evento ObjectCreated
   │
   ▼
AWS Lambda
   │
   ├── Redimensiona imagem
   ├── Gera miniatura
   ├── Salva no S3
   └── Registra log no CloudWatch
```

---

# Benefícios da Arquitetura

- Redução de custos operacionais.
- Processamento automático de arquivos.
- Escalabilidade sem intervenção manual.
- Integração simples com outros serviços da AWS.
- Alta disponibilidade e confiabilidade.
- Desenvolvimento rápido de soluções orientadas a eventos.

---

# Conclusão

A integração entre **AWS Lambda** e **Amazon S3** é uma das arquiteturas Serverless mais utilizadas na AWS. Ela permite automatizar tarefas baseadas em eventos de forma eficiente, escalável e com baixo custo. Essa abordagem é ideal para processamento de arquivos, automação de fluxos, integração entre serviços e construção de aplicações modernas orientadas a eventos.