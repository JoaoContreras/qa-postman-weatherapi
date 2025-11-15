# qa-postman-weatherapi
Portfólio de testes de API com Postman usando a WeatherAPI (GET e testes automatizados com environments)

Projeto simples usando **Postman**

## Endpoints usados

Todos os endpoints são baseados em:

- `https://api.weatherapi.com/v1`

Neste projeto a collection contém:

1. **Current Weather (tempo atual)**
   - `GET /current.json?key={{api_key}}&q={{city}}`
   - Usa variáveis de ambiente `api_key` e `city`
   - Testes:
     - Status code = 200
     - Resposta contém `location.name`
     - Resposta contém `current.temp_c`

2. **Forecast 3 dias (previsão)**
   - `GET /forecast.json?key={{api_key}}&q={{city}}&days=3&aqi=no&alerts=no`
   - Testes:
     - Status code = 200
     - Resposta contém `forecast.forecastday`
     - Garante que existem pelo menos 3 dias de previsão

3. **Search City (autocomplete)**
   - `GET /search.json?key={{api_key}}&q={{search_query}}`
   - Testes:
     - Status code = 200
     - Resposta é um array
     - Primeiro item tem `name` e `country`

## Como rodar

### 1. Criar conta e pegar API key

1. Acesse [https://www.weatherapi.com/](https://www.weatherapi.com/)
2. Crie uma conta gratuita
3. Copie sua **API key**

4. ### 2. Importar Environment e Collection no Postman

1. Abra o Postman
2. Vá em **Environments > Import** e selecione:
   - `environments/weatherapi-local.postman_environment.json`
3. Vá em **Collections > Import** e selecione:
   - `collections/weatherapi-postman-collection.json`
4. No Postman, selecione o environment **WeatherAPI – Local**
5. Edite a variável `api_key` no ambiente e coloque a sua chave real (localmente, não no Git)

### 3. Executar os testes

1. Abra a collection **WeatherAPI – Portfolio**
2. Escolha uma request (ex.: **01 – Current Weather**)
3. Clique em **Send**
4. Vá até a aba **Tests** (abaixo da resposta) e confira os resultados dos testes

Você também pode usar o **Runner** do Postman para executar a collection inteira e ver todos os testes passando de uma vez.

## Tecnologias / Ferramentas

- Postman (requisições HTTP e testes)
- WeatherAPI (dados de clima)
- JSON (requests e responses)
