# Ferramentas

Tesla expõe 11 ferramentas.

### 1. `tesla_veiculos`
**Input**: `account` (opcional)

Lista os carros da conta Tesla conectada: VIN, nome, modelo, se está online ou dormindo, e se a chave virtual do app já está pareada (sem ela os comandos não chegam ao carro).

### 2. `tesla_estado`
**Input**: `veiculos` (opcional), `acordar` (opcional), `account` (opcional)

Estado do carro: bateria (%), autonomia (km), carga (conectado, carregando, limite, tempo restante), clima (temperaturas, ar ligado), travas, portas e janelas, odômetro e software.

### 3. `tesla_localizacao`
**Input**: `veiculos` (opcional), `acordar` (opcional), `account` (opcional)

Localização atual do carro: latitude, longitude, direção e velocidade, e o destino ativo na navegação quando houver.

### 4. `tesla_acordar`
**Input**: `veiculos` (opcional), `account` (opcional)

Acorda o carro (sai do modo dormindo) e espera até ~30 s ficar online.

### 5. `tesla_definir_destino`
**Input**: `veiculos` (opcional), `endereco` (opcional), `latitude` (opcional), `longitude` (opcional), `account` (opcional)

Envia um destino para a navegação do carro, que começa a rota na tela.

### 6. `tesla_ir_supercharger`
**Input**: `veiculos` (opcional), `account` (opcional)

Inicia a navegação do carro até o Supercharger mais próximo.

### 7. `tesla_travar`
**Input**: `veiculos` (opcional), `account` (opcional)

Trava as portas do carro. Acorda o carro se precisar.

### 8. `tesla_destravar`
**Input**: `veiculos` (opcional), `account` (opcional)

DESTRAVA as portas do carro, com efeito físico imediato: qualquer pessoa ao lado do carro consegue abri-lo.

### 9. `tesla_clima`
**Input**: `veiculos` (opcional), `ligar`, `temperatura_c` (opcional), `account` (opcional)

Liga ou desliga o ar-condicionado do carro e, opcionalmente, define a temperatura (°C, motorista e passageiro).

### 10. `tesla_carga`
**Input**: `veiculos` (opcional), `acao` (opcional), `limite_percent` (opcional), `account` (opcional)

Controla a carga: `iniciar` ou `parar` a carga (o cabo precisa estar conectado) e/ou ajustar o limite de carga em % (50 a 100).

### 11. `tesla_buzinar_piscar`
**Input**: `veiculos` (opcional), `acao`, `account` (opcional)

Buzina ou pisca os faróis do carro, para achá-lo num estacionamento.

## Prompts de exemplo

```
Manda o Ferry Building, San Francisco, California para a navegação do meu Tesla
Quanto de bateria e autonomia meu carro tem agora?
Onde meu carro está estacionado?
Liga o ar do carro em 21 graus
Me leva até o Supercharger mais próximo
Coloca o limite de carga em 80% e começa a carregar
```
