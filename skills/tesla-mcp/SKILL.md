---
name: tesla-mcp
description: Skill da REST API do Tesla na MCP.AI: 11 endpoints em /api/tesla. Converse com o seu **Tesla** a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **Fleet API oficial da Tesla**, com a **sua própria conta Tesla** (OAuth) e **sem intermediário**. O destaque é a **navegação**: "manda esse endereço pro meu carro" coloca a rota na tela do carro, a partir de um endereço, de coordenadas ou do Supercharger mais próximo. Também lê **bateria, autonomia, carga, clima, travas e localização**, e manda comandos: travar e destravar, ligar o ar e ajustar a temperatura, iniciar ou parar a carga e o limite, buzinar e piscar. Os comandos são assinados pelo **Vehicle Command Protocol** da Tesla. Pague por uso com crédito pré-pago. **Não afiliado à Tesla.** Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# Tesla — REST API skill

Você tem acesso à **Tesla** REST API na MCP.AI.

> Converse com o seu **Tesla** a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **Fleet API oficial da Tesla**, com a **sua própria conta Tesla** (OAuth) e **sem intermediário**. O destaque é a **navegação**: "manda esse endereço pro meu carro" coloca a rota na tela do carro, a partir de um endereço, de coordenadas ou do Supercharger mais próximo. Também lê **bateria, autonomia, carga, clima, travas e localização**, e manda comandos: travar e destravar, ligar o ar e ajustar a temperatura, iniciar ou parar a carga e o limite, buzinar e piscar. Os comandos são assinados pelo **Vehicle Command Protocol** da Tesla. Pague por uso com crédito pré-pago. **Não afiliado à Tesla.**

## Base URL

```
https://api.mcp.ai/api/tesla
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/tesla/acordar \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/tesla/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (11)

#### `tesla_acordar`

Acorda o carro (sai do modo dormindo) e espera até ~30 s ficar online. _(POST /api/tesla/acordar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_buzinar_piscar`

Buzina ou pisca os faróis do carro, para achá-lo num estacionamento. _(POST /api/tesla/buzinar/piscar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `acao` | string | Sim | buzinar ou piscar os faróis. (buzinar, piscar) |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_carga`

Controla a carga: `iniciar` ou `parar` a carga (o cabo precisa estar conectado) e/ou ajustar o limite de carga em % (50 a 100). _(POST /api/tesla/carga)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `acao` | string | Não | iniciar ou parar a carga. (iniciar, parar) |
| `limite_percent` | integer | Não | Novo limite de carga em % (50 a 100). |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_clima`

Liga ou desliga o ar-condicionado do carro e, opcionalmente, define a temperatura (°C, motorista e passageiro). _(POST /api/tesla/clima)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `ligar` | boolean | Sim | true liga o clima, false desliga. |
| `temperatura_c` | number | Não | Temperatura desejada em °C (15 a 28). Só vale com ligar=true. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_definir_destino`

Envia um destino para a navegação do carro, que começa a rota na tela. _(POST /api/tesla/definir/destino)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `endereco` | string | Não | Endereço ou nome do lugar, ex.: "Av. Paulista, 1000, São Paulo". |
| `latitude` | number | Não | Latitude do destino (graus decimais). |
| `longitude` | number | Não | Longitude do destino (graus decimais). |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_destravar`

DESTRAVA as portas do carro, com efeito físico imediato: qualquer pessoa ao lado do carro consegue abri-lo. _(POST /api/tesla/destravar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_estado`

Estado do carro: bateria (%), autonomia (km), carga (conectado, carregando, limite, tempo restante), clima (temperaturas, ar ligado), travas, portas e janelas, odômetro e software. _(POST /api/tesla/estado)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `acordar` | boolean | Não | Acorda o carro se estiver dormindo antes de ler (padrão false). Acordar leva até ~30 s, gasta bateria e custa mais. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_ir_supercharger`

Inicia a navegação do carro até o Supercharger mais próximo. _(POST /api/tesla/ir/supercharger)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_localizacao`

Localização atual do carro: latitude, longitude, direção e velocidade, e o destino ativo na navegação quando houver. _(POST /api/tesla/localizacao)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `acordar` | boolean | Não | Acorda o carro se estiver dormindo antes de ler (padrão false). Acordar leva até ~30 s, gasta bateria e custa mais. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_travar`

Trava as portas do carro. Acorda o carro se precisar. _(POST /api/tesla/travar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `veiculos` | string[] | Não | VINs ou nomes dos carros (ver tesla_veiculos). Pode omitir quando a conta tem um carro só. |
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

#### `tesla_veiculos`

Lista os carros da conta Tesla conectada: VIN, nome, modelo, se está online ou dormindo, e se a chave virtual do app já está pareada (sem ela os comandos não chegam ao carro). _(POST /api/tesla/veiculos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Só quando há mais de uma conta Tesla conectada: e-mail, id ou parte do nome da conta. Ver tesla_veiculos. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_tesla` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
