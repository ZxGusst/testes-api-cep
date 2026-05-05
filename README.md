# Testes de API - Consulta de CEP com Postman

Exercício de testes automatizados de API REST usando Postman, com foco em validação de status HTTP, corpo da resposta e tempo de resposta.

**API:** [BrasilAPI](https://brasilapi.com.br) — gratuita, sem token, sem cadastro.

## Estrutura

```
├── CPF-API-Collection.postman_collection.json   # Collection com 6 casos de teste
└── CPF-API-Environment.postman_environment.json # Variáveis de ambiente
```

## Como usar

1. Importe os dois arquivos no Postman (File > Import)
2. Selecione o environment **"CPF API - Ambiente"** no canto superior direito
3. Execute a collection com o Collection Runner

## Casos de Teste

| ID    | Cenário                              | Tipo     | Validações                           |
|-------|--------------------------------------|----------|--------------------------------------|
| CT-01 | CEP válido (Praça da Sé - SP)        | Positivo | Status 200, campos cep/state, tempo  |
| CT-02 | CEP válido - estrutura completa      | Positivo | Status 200, JSON válido, city/street |
| CT-03 | CEP com letras (formato inválido)    | Negativo | Status 400, mensagem de erro         |
| CT-04 | CEP inexistente (99999999)           | Negativo | Status 404, campo message            |
| CT-05 | CEP com menos de 8 dígitos           | Borda    | Status 400, corpo não vazio          |
| CT-06 | CEP com mais de 8 dígitos            | Borda    | Status 400, corpo não vazio          |

## Endpoint utilizado

```
GET https://brasilapi.com.br/api/cep/v2/{cep}
```

## Rodando via Newman (linha de comando)

```bash
npm install -g newman

newman run CPF-API-Collection.postman_collection.json \
  -e CPF-API-Environment.postman_environment.json
```
