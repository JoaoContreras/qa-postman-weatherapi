Projeto simples usando **Postman** para consumir a API de clima e mostrar:

- uso de **variáveis de ambiente**
- **parâmetros de query**
- **scripts de teste** em JavaScript
- gravação de valores da resposta em variáveis (`pm.environment.set`)

---

## Endpoints usados

Todos os endpoints são baseados em:

- `https://api.openweathermap.org/data/2.5`

Neste projeto a collection contém:

1. **Clima atual (weather) – cidade fixa**
   - `GET /weather?q={{city}}&lang={{lang}}&units={{units}}&appid={{api_key}}`
   - Usa variáveis de ambiente:
     - `base_url`
     - `city`
     - `lang`
     - `units`
     - `api_key`
   - Exemplo com `city = London`, `lang = pt_br`, `units = metric`

### Testes automatizados no Postman

Na aba de scripts pós-resposta, os testes verificam:

- `Status code = 200`
- Resposta é um JSON válido
- Resposta contém o campo `name` (nome da cidade)
- A cidade retornada é `London`
- Resposta contém `main.temp` (temperatura)
- A temperatura é armazenada em uma variável de ambiente:
  - `last_temp_london`

Exemplo de script de teste:

```javascript
// 1) Status code
pm.test("Status code é 200", function () {
    pm.response.to.have.status(200);
});

// 2) Resposta é JSON válida
let jsonData;
pm.test("Resposta é JSON válida", function () {
    jsonData = pm.response.json();
});

// 3) Tem campo 'name' (cidade)
pm.test("Resposta tem campo name (cidade)", function () {
    pm.expect(jsonData).to.have.property("name");
});

// 4) Cidade retornada é London
pm.test("Cidade retornada é London", function () {
    pm.expect(jsonData.name).to.eql("London");
});

// 5) Tem temperatura em main.temp
pm.test("Resposta tem main.temp", function () {
    pm.expect(jsonData).to.have.property("main");
    pm.expect(jsonData.main).to.have.property("temp");
});

// 6) Guardar temperatura em variável de ambiente
pm.environment.set("last_temp_london", jsonData.main.temp);
