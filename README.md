# Microsserviço de Validação de CPF com Azure Functions

## Descrição
Este projeto tem como objetivo desenvolver um microsserviço eficiente, escalável e econômico para validação de CPFs, utilizando arquitetura serverless com Azure Functions.

## Estrutura de Pastas
```
cpf-validator/
├── .azure-pipelines/
│   └── azure-pipelines.yml
├── cpf_validator/
│   └── __init__.py
├── tests/
│   └── test_validator.py
├── requirements.txt
└── README.md
```

## Código da Função (cpf_validator/__init__.py)
```python
import re
import azure.functions as func

def validate_cpf(cpf):
    cpf = re.sub(r'[^0-9]', '', cpf)
    if len(cpf) != 11 or cpf == cpf[0] * 11:
        return False

    for i in range(9, 11):
        value = sum(int(cpf[num]) * ((i+1) - num) for num in range(0, i))
        check = ((value * 10) % 11) % 10
        if check != int(cpf[i]):
            return False
    return True

def main(req: func.HttpRequest) -> func.HttpResponse:
    cpf = req.params.get('cpf')
    if not cpf:
        return func.HttpResponse("CPF não fornecido.", status_code=400)

    if validate_cpf(cpf):
        return func.HttpResponse("CPF válido.", status_code=200)
    else:
        return func.HttpResponse("CPF inválido.", status_code=400)
```

## Testes Unitários (tests/test_validator.py)
```python
from cpf_validator import validate_cpf

def test_valid_cpf():
    assert validate_cpf("52998224725") == True

def test_invalid_cpf():
    assert validate_cpf("12345678900") == False
```

## Requisitos (requirements.txt)
```
azure-functions
```

## Pipeline CI/CD (azure-pipelines.yml)
```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.10'
    addToPath: true

- script: |
    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    pip install pytest
    pytest tests/
  displayName: 'Instalar dependências e rodar testes'

- task: AzureFunctionApp@1
  inputs:
    azureSubscription: '<nome-da-sua-conexao>'
    appType: 'functionAppLinux'
    appName: '<nome-da-sua-funcao>'
    package: '$(System.DefaultWorkingDirectory)/cpf-validator'
```

## Implantação
Configure sua Azure Function no portal do Azure e conecte o repositório com Azure DevOps para que o pipeline execute automaticamente a cada push.

---

*Este projeto oferece uma solução moderna e econômica para validação de CPFs com alta disponibilidade e escalabilidade.*
