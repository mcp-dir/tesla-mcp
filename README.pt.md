# Tesla

### MCP para Tesla, mande um destino pro carro e controle tudo em linguagem natural

Converse com o seu **Tesla** a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **Fleet API oficial da Tesla**, com a **sua própria conta Tesla** (OAuth) e **sem intermediário**. O destaque é a **navegação**: "manda esse endereço pro meu carro" coloca a rota na tela do carro, a partir de um endereço, de coordenadas ou do Supercharger mais próximo. Também lê **bateria, autonomia, carga, clima, travas e localização**, e manda comandos: travar e destravar, ligar o ar e ajustar a temperatura, iniciar ou parar a carga e o limite, buzinar e piscar. Os comandos são assinados pelo **Vehicle Command Protocol** da Tesla. Pague por uso com crédito pré-pago. **Não afiliado à Tesla.**

- 🧭 **Mande um destino pro carro**: endereço, coordenadas ou o Supercharger mais próximo, direto na navegação
- 🔋 **Bateria, autonomia e carga**: nível, autonomia em km, status da carga, limite e tempo para completar
- 📍 **Localização**: onde o carro está, direção e velocidade, e o destino da rota ativa
- ❄️ **Clima**: ligar ou desligar e ajustar a temperatura antes de sair
- 🔒 **Travas, buzina e faróis**: travar, destravar (com confirmação), buzinar ou piscar para achar o carro no estacionamento
- 😴 **Respeita o modo dormindo**: leitura nunca acorda o carro sem você pedir; comando acorda só quando precisa
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[English version](README.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Tesla` e **URL** `https://api.mcp.ai/p_tesla`.

### Cursor

[➕ Instalar Tesla no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=tesla&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF90ZXNsYSJ9)

### VS Code (Copilot Chat)

[➕ Instalar Tesla no VS Code](vscode:mcp/install?name=tesla&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_tesla%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_tesla
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Manda o Ferry Building, San Francisco, California para a navegação do meu Tesla
Quanto de bateria e autonomia meu carro tem agora?
Onde meu carro está estacionado?
Liga o ar do carro em 21 graus
Me leva até o Supercharger mais próximo
Coloca o limite de carga em 80% e começa a carregar
```

---

## 11 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)


---

## O que dá para perguntar

| Área | Cobertura | Escrita |
|---|---|---|
| **Navegação** | Mandar endereço ou coordenadas para a navegação do carro, rota até o Supercharger mais próximo | Escrita |
| **Estado do carro** | Bateria, autonomia, status e limite da carga, clima e temperaturas, travas, portas e janelas, odômetro, versão do software | Leitura |
| **Localização** | Coordenadas, direção, velocidade, destino da rota ativa e previsão de chegada | Leitura |
| **Clima** | Ligar/desligar e temperatura do motorista e do passageiro | Escrita |
| **Carga** | Iniciar/parar a carga, limite de carga (50 a 100%) | Escrita |
| **Segurança e achar o carro** | Travar, destravar, buzinar, piscar os faróis | Escrita |
| **Frota** | Todos os carros da conta, online ou dormindo, e se a chave virtual está pareada | Leitura |

### Antes de conectar, três avisos honestos

1. **Comando precisa da chave virtual.** Depois de autorizar, abra
   `https://www.tesla.com/_ak/api.mcp.ai` no celular (com o app da Tesla) e
   aprove a chave em cada carro. Leitura funciona sem ela; comando não.
2. **Regiões.** A Fleet API da Tesla atende contas da América do Norte/Ásia-Pacífico
   e da Europa. Contas de outras regiões (por exemplo, Brasil) podem não conectar.
3. **Carro dormindo.** Leitura nunca acorda o carro sozinha, porque acordar custa
   mais e gasta bateria. Peça (`acordar: true`) ou mande um comando, que acorda
   o carro quando precisa.

---

## Preços

Pré-pago (carteira de créditos), paga por uso. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Sub-processadores**: Tesla, Inc., o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**É o MCP oficial da Tesla?**
Não. Este é um MCP **independente**, que fala com a Fleet API oficial da Tesla usando a sua própria conta Tesla. **Não é afiliado à Tesla** e não implica parceria. Tesla é marca do seu titular, citada aqui de forma nominativa.

**Tem algum intermediário entre mim e o meu carro?**
Nenhum serviço como Tessie ou Teslemetry. As chamadas vão do servidor do mcp.ai direto para a Fleet API da Tesla, e os comandos são assinados pelo Vehicle Command Protocol com a chave do nosso app, que você aprova no celular.

**Por que um comando falha no meu carro?**
Quase sempre a chave virtual ainda não foi pareada. Abra https://www.tesla.com/_ak/api.mcp.ai no celular com o app da Tesla e aprove a chave para aquele carro. A ferramenta devolve esse link quando acontece.

**Onde ficam os meus tokens?**
Cifrados, e usados só para chamar a Fleet API da Tesla. Eles não aparecem em resposta de ferramenta nem em log. Você pode revogar o acesso a qualquer momento na sua conta Tesla.

**Quanto custa?**
Pague por uso com crédito pré-pago, com preço baseado nas taxas por requisição da própria Tesla (dado, comando, acordar). As primeiras chamadas são grátis para testar.


---

## Suporte

- 📧 [tesla@mcp.ai](mailto:tesla@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/tesla-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_tesla` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
