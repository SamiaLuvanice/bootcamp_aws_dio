# DevOps na AWS

## O que é DevOps?

DevOps é uma cultura e um conjunto de práticas que unem desenvolvimento
(Dev) e operações (Ops), com foco em automação, integração contínua,
entrega contínua e monitoramento.

## Principais serviços da AWS

-   **AWS CodeCommit**: Repositório Git gerenciado.
-   **AWS CodeBuild**: Compilação e testes automatizados.
-   **AWS CodeDeploy**: Implantação automatizada.
-   **AWS CodePipeline**: Orquestra pipelines de CI/CD.
-   **Amazon EC2**: Servidores virtuais.
-   **Amazon ECS / EKS**: Orquestração de contêineres.
-   **AWS Lambda**: Execução serverless.
-   **Amazon CloudWatch**: Monitoramento e logs.
-   **AWS CloudFormation**: Infraestrutura como Código (IaC).
-   **AWS Systems Manager**: Gerenciamento de instâncias.

## Fluxo típico de CI/CD

1.  Desenvolvedor envia código ao repositório.
2.  CodePipeline inicia automaticamente.
3.  CodeBuild executa build e testes.
4.  Artefatos são gerados.
5.  CodeDeploy realiza o deploy.
6.  CloudWatch monitora a aplicação.

## Boas práticas

-   Automatizar testes.
-   Utilizar Infraestrutura como Código.
-   Implementar monitoramento e alertas.
-   Armazenar segredos no AWS Secrets Manager.
-   Aplicar o princípio do menor privilégio no IAM.

## Ferramentas complementares

-   Docker
-   Kubernetes
-   Terraform
-   GitHub Actions
-   Ansible

## Conclusão

A AWS oferece um ecossistema completo para implementar DevOps,
permitindo criar pipelines confiáveis, automatizar implantações e
escalar aplicações com segurança.
