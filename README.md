# Microsserviço de Validação de CPF com Azure Functions

## Descrição
Este projeto tem como objetivo desenvolver um microsserviço eficiente, escalável e econômico para validação de CPFs, utilizando arquitetura serverless. A aplicação será construída com base em princípios modernos de computação em nuvem, garantindo alta disponibilidade, baixo custo operacional e facilidade de manutenção.

## Tecnologias Utilizadas
- **Azure Functions**: Plataforma serverless da Microsoft Azure para execução de funções sob demanda.
- **Python**: Linguagem de programação utilizada para implementar a lógica de validação de CPF.
- **Azure Storage**: Para armazenar logs e dados temporários.
- **Azure Monitor**: Para monitoramento e diagnóstico da aplicação.

## Arquitetura
A arquitetura será baseada em eventos, onde cada requisição HTTP acionará uma função do Azure responsável por validar o CPF informado. A função será executada de forma isolada, garantindo escalabilidade automática e cobrança apenas pelo tempo de execução.

## Funcionalidades
- Validação de formato e dígitos verificadores do CPF.
- Resposta em JSON com status da validação.
- Logs de requisições para análise posterior.

## Benefícios
- **Alta disponibilidade**: Infraestrutura gerenciada pela Azure.
- **Baixo custo**: Pagamento apenas pelo tempo de execução das funções.
- **Escalabilidade automática**: Ajuste de recursos conforme demanda.
- **Fácil manutenção**: Separação clara de responsabilidades e código modular.

## Próximos Passos
1. Configuração do ambiente no Azure.
2. Desenvolvimento da função de validação de CPF.
3. Testes unitários e de integração.
4. Implantação e monitoramento.

---

*Este projeto é ideal para empresas que desejam validar CPFs de forma rápida e confiável, sem a necessidade de manter servidores dedicados.*
