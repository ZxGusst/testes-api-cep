# Testes de API - Consulta de CPF com Postman

Exercício de testes automatizados de API REST usando Postman, com foco em validação de status HTTP, corpo da resposta e tempo de resposta.

## Estrutura

```
├── CPF-API-Collection.postman_collection.json   # Collection com 6 casos de teste
└── CPF-API-Environment.postman_environment.json # Variáveis de ambiente
```

## Como usar

1. Importe os dois arquivos no Postman (File > Import)
2. Selecione o environment **"CPF API - Ambiente"** no canto superior direito
3. Atualize a variável `base_url` com sua URL e token da API
4. Execute a collection com o Runner (Collection Runner ou Newman)

## Casos de Teste

| ID    | Cenário                              | Tipo     | Validações                          |
|-------|--------------------------------------|----------|-------------------------------------|
| CT-01 | CPF válido                           | Positivo | Status 200, campo cpf, tempo < 2s   |
| CT-02 | CPF válido - estrutura completa      | Positivo | Status 200, JSON válido, tipos      |
| CT-03 | CPF com formato inválido (letras)    | Negativo | Status 4xx, mensagem de erro        |
| CT-04 | CPF com dígitos verificadores erros  | Negativo | Status 4xx ou valid=false           |
| CT-05 | CPF com todos dígitos iguais         | Borda    | Rejeição por regra da Receita Fed.  |
| CT-06 | Requisição sem CPF                   | Borda    | Status 400 ou 404                   |

## Rodando via Newman (linha de comando)

```bash
npm install -g newman

newman run CPF-API-Collection.postman_collection.json \
  -e CPF-API-Environment.postman_environment.json \
  --reporters cli,junit \
  --reporter-junit-export resultado.xml
```

## API utilizada

[api.cpfcnpj.com.br](https://api.cpfcnpj.com.br) — plano gratuito disponível para testes.
