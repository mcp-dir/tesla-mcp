# Tesla

### Tesla MCP, send a destination to your car and control it in plain language

Talk to your **Tesla** from Claude, ChatGPT or any MCP client. It runs on the **official Tesla Fleet API**, with **your own Tesla account** (OAuth) and **no third-party relay** in the middle. The highlight is **navigation**: "send this address to my car" puts the route on the car's screen, from a street address, coordinates or the nearest Supercharger. It also reads **battery, range, charging, climate, locks and location**, and runs commands: lock and unlock, climate on/off and temperature, start/stop charging and charge limit, honk and flash. Commands are signed with Tesla's **Vehicle Command Protocol**. Pay per use with prepaid credits. **Not affiliated with Tesla.**

- 🧭 **Send a destination to the car**: street address, coordinates or the nearest Supercharger, straight to the car's navigation
- 🔋 **Battery, range and charging**: state of charge, range in km, charging status, limit and time to full
- 📍 **Location**: where the car is, heading and speed, and the active route destination
- ❄️ **Climate**: turn it on or off and set the temperature before you leave
- 🔒 **Locks, honk and lights**: lock, unlock (with a confirmation step), honk or flash to find it in a parking lot
- 😴 **Sleep-aware**: reads never wake the car unless you ask; commands wake it only when needed
- 💬 **Works with any MCP client**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[Versão em português](README.pt.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `Tesla` and **URL** `https://api.mcp.ai/p_tesla`.

### Cursor

[➕ Install Tesla in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=tesla&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF90ZXNsYSJ9)

### VS Code (Copilot Chat)

[➕ Install Tesla in VS Code](vscode:mcp/install?name=tesla&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_tesla%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_tesla
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
Send the Ferry Building, San Francisco, California to my Tesla's navigation
How much battery and range does my car have right now?
Where is my car parked?
Turn on the climate at 21°C
Take me to the nearest Supercharger
Set the charge limit to 80% and start charging
```

---

## 11 tools available

| Tool | Description |
|---|---|
| `tesla_veiculos` | Lista os carros da conta Tesla conectada: VIN, nome, modelo, se está online ou dormindo, e se a chave virtual do app já está pareada (sem ela os comandos não chegam ao carro). |
| `tesla_estado` | Estado do carro: bateria (%), autonomia (km), carga (conectado, carregando, limite, tempo restante), clima (temperaturas, ar ligado), travas, portas e janelas, odômetro e software. |
| `tesla_localizacao` | Localização atual do carro: latitude, longitude, direção e velocidade, e o destino ativo na navegação quando houver. |
| `tesla_acordar` | Acorda o carro (sai do modo dormindo) e espera até ~30 s ficar online. |
| `tesla_definir_destino` | Envia um destino para a navegação do carro, que começa a rota na tela. |
| `tesla_ir_supercharger` | Inicia a navegação do carro até o Supercharger mais próximo. |
| `tesla_travar` | Trava as portas do carro. Acorda o carro se precisar. |
| `tesla_destravar` | DESTRAVA as portas do carro, com efeito físico imediato: qualquer pessoa ao lado do carro consegue abri-lo. |
| `tesla_clima` | Liga ou desliga o ar-condicionado do carro e, opcionalmente, define a temperatura (°C, motorista e passageiro). |
| `tesla_carga` | Controla a carga: `iniciar` ou `parar` a carga (o cabo precisa estar conectado) e/ou ajustar o limite de carga em % (50 a 100). |
| `tesla_buzinar_piscar` | Buzina ou pisca os faróis do carro, para achá-lo num estacionamento. |

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)


---

## What you can ask

| Area | Coverage | Writes |
|---|---|---|
| **Navigation** | Send a street address or coordinates to the car's navigation, route to the nearest Supercharger | Write |
| **Vehicle state** | Battery, range, charging status and limit, climate and temperatures, locks, doors and windows, odometer, software version | Read |
| **Location** | Coordinates, heading, speed, active route destination and ETA | Read |
| **Climate** | On/off and driver/passenger temperature | Write |
| **Charging** | Start/stop charging, charge limit (50 to 100%) | Write |
| **Security and finding the car** | Lock, unlock, honk, flash the lights | Write |
| **Fleet** | Every car on the account, online or asleep, and whether the virtual key is paired | Read |

### Before connecting, three honest notes

1. **Commands need the virtual key.** After you authorize, open
   `https://www.tesla.com/_ak/api.mcp.ai` on your phone (Tesla app installed)
   and approve the key for each car. Reads work without it; commands do not.
2. **Regions.** The Tesla Fleet API serves accounts in North America/Asia-Pacific
   and Europe. Accounts in other regions (for example Brazil) may not connect.
3. **Sleeping cars.** Reads never wake the car on their own, because waking costs
   more and uses battery. Ask for it (`acordar: true`) or just send a command,
   which wakes the car when it has to.

---

## Pricing

Prepaid credit wallet, pay per use. See [docs/precos.md](docs/precos.md) (PT-BR).

---

## Privacy & data protection

- **Sub-processors**: Tesla, Inc., the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is this Tesla's official MCP?**
No. This is an **independent** MCP that talks to Tesla's official Fleet API with your own Tesla account. It is **not affiliated with Tesla** and does not imply a partnership. Tesla is a trademark of its owner, cited here nominatively.

**Is there a third party between me and my car?**
No relay service like Tessie or Teslemetry. Calls go from the mcp.ai server straight to the Tesla Fleet API, and commands are signed with Tesla's Vehicle Command Protocol using our app key, which you approve on your phone.

**Why does a command fail on my car?**
Almost always the virtual key is not paired yet. Open https://www.tesla.com/_ak/api.mcp.ai on your phone with the Tesla app installed and approve it for that car. The tool returns this link when it happens.

**Where are my tokens stored?**
Encrypted, and used only to call the Tesla Fleet API. They never show up in a tool response or in logs. You can revoke access anytime in your Tesla account.

**How much does it cost?**
Pay per use with prepaid credits, priced on Tesla's own per-request fees (data, command, wake). Your first calls are free to try it.


---

## Support

- 📧 [tesla@mcp.ai](mailto:tesla@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/tesla-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_tesla` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
