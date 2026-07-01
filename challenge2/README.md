# Introdução ao AWS Step Functions

Este documento apresenta, de forma breve e prática, os principais conceitos do **AWS Step Functions**, um serviço usado para orquestrar aplicações serverless e fluxos de trabalho distribuídos na AWS.

---

## O que é o AWS Step Functions

O AWS Step Functions é um serviço de orquestração de workflows que permite coordenar diferentes serviços da AWS, como **Lambda**, **SQS**, **SNS**, **DynamoDB**, **ECS**, **Glue** e outros.

Ele organiza a execução de tarefas em um fluxo visual e declarativo, facilitando o controle de etapas, condições, paralelismo, tratamento de erros e monitoramento.

---

## Conceitos principais

- **State Machine:** definição do fluxo de execução. Ela descreve as etapas, transições e regras do processo.
- **States:** cada etapa do fluxo. Um estado pode executar uma tarefa, decidir caminhos, aguardar, repetir ou encerrar.
- **Task:** estado que executa uma ação, normalmente chamando um serviço AWS ou uma função Lambda.
- **Choice:** estado condicional, usado para tomar decisões com base em regras.
- **Pass:** estado que apenas repassa dados sem executar processamento.
- **Wait:** estado que pausa o fluxo por um tempo definido.
- **Parallel:** executa várias etapas ao mesmo tempo.
- **Map:** processa uma lista de itens, aplicando o mesmo fluxo para cada elemento.
- **Input e Output:** dados que entram e saem de cada estado durante a execução.

---

## Tipos de workflow

### Standard Workflows

- Indicados para processos de longa duração.
- Suportam execução que pode durar até 1 ano.
- Oferecem histórico detalhado e forte rastreabilidade.
- Ideais para orquestração crítica, aprovações e processos empresariais.

### Express Workflows

- Indicados para fluxos de alta frequência e curta duração.
- Têm menor custo em cenários de grande volume.
- São ideais para eventos rápidos, automações e processamento em tempo real.

---

## Como funciona na prática

1. Um evento ou aplicação inicia a máquina de estados.
2. O Step Functions executa a primeira etapa definida no fluxo.
3. Cada estado decide o próximo passo com base no resultado atual.
4. O workflow pode tratar erros, repetir tentativas e seguir caminhos diferentes.
5. Ao final, o serviço registra o resultado da execução.

---

## Exemplo de uso

Um cenário comum é o processamento de pedidos:

1. Validar o pedido.
2. Reservar estoque.
3. Processar pagamento.
4. Confirmar envio.
5. Notificar o cliente.

Nesse caso, o Step Functions garante que cada etapa seja executada na ordem correta e que falhas sejam tratadas de forma previsível.

---

## Vantagens

- Simplifica a orquestração de serviços distribuídos.
- Reduz a necessidade de código de controle manual.
- Facilita observabilidade com visualização do fluxo.
- Permite tratamento de erros, retries e timeouts.
- Separa a lógica de negócio da lógica de coordenação.

---

## Boas práticas

- Mantenha as máquinas de estados pequenas e com responsabilidade clara.
- Use nomes descritivos para os estados.
- Defina tratamento de erro com `Retry` e `Catch`.
- Evite fluxos excessivamente complexos sem necessidade.
- Planeje bem o formato dos dados entre os estados.
- Use Standard ou Express de acordo com o tempo de execução e o volume esperado.

---

## Exemplo simples de state machine

O exemplo abaixo mostra um fluxo básico com três etapas: validar pedido, processar pagamento e finalizar.

```json
{
	"Comment": "Fluxo simples de processamento de pedido",
	"StartAt": "ValidarPedido",
	"States": {
		"ValidarPedido": {
			"Type": "Task",
			"Resource": "arn:aws:lambda:us-east-1:123456789012:function:validarPedido",
			"Next": "ProcessarPagamento"
		},
		"ProcessarPagamento": {
			"Type": "Task",
			"Resource": "arn:aws:lambda:us-east-1:123456789012:function:processarPagamento",
			"Next": "FinalizarPedido"
		},
		"FinalizarPedido": {
			"Type": "Succeed"
		}
	}
}
```

---

## Quando usar

Use Step Functions quando for necessário:

- coordenar múltiplos serviços AWS;
- controlar etapas com dependências entre si;
- tratar falhas de forma explícita;
- executar fluxos paralelos ou iterativos;
- ter visibilidade clara do andamento do processo.

---

## Links úteis

- Documentação oficial: https://docs.aws.amazon.com/step-functions/
- Conceitos de state machines: https://docs.aws.amazon.com/step-functions/latest/dg/concepts-state-machine.html
- Tipos de workflow: https://docs.aws.amazon.com/step-functions/latest/dg/choosing-workflow-type.html
- Diagrama do fluxo: [step-functions-fluxo.drawio](step-functions-fluxo.drawio)

---

## Conclusão

O AWS Step Functions é uma solução muito útil para organizar processos complexos de forma visual, confiável e escalável. Ele ajuda a conectar serviços da AWS com menos código e mais controle sobre cada etapa do fluxo.
