# 🪙 PLT Blockchain

> "Poder para crear, libertad para transaccionar, tecnología al servicio de la gente." 

**PLT** es una blockchain soberana construida con **Cosmos SDK** y el motor de consenso **CometBFT**. Una red moderna, abierta y gobernada por quienes la utilizan.

---

## 🌌 Visión

- **Poder** para quienes construyen y resguardan la red.
- **Libertad** financiera para mover valor sin permisos ni intermediarios.
- **Tecnología** confiable, modular y auditable, preparada para escalar economías reales.

---

## ⚙️ Requisitos previos

- Go **1.22+**
- GNU Make, **git**, **curl**, **jq**
- Linux o macOS

---

## 🚀 Instalación rápida

```bash
# Obtener el código fuente
git clone https://github.com/nobelaar/pltnet
cd pltnet

# Preparar dependencias
go mod tidy

# Compilar el binario principal
go build -o ~/go/bin/pltd ./cmd/pltd

# Confirmar versión
env PATH="$HOME/go/bin:$PATH" pltd version
```

> 💡 Asegúrate de que `~/go/bin` esté en tu `PATH` para invocar `pltd` desde cualquier directorio.

---

## 🧭 Guía general de participantes

PLT se sostiene por cuatro pilares de participación coordinada:

1. **Usuarios**: exploran la red, gestionan cuentas y realizan transacciones soberanas.
2. **Operadores de nodos**: garantizan disponibilidad, replican el estado y difunden bloques.
3. **Validadores**: aseguran el consenso, protegen el protocolo y reciben recompensas.
4. **Desarrolladores**: expanden las capacidades de la cadena y construyen aplicaciones soberanas.

Cada rol cuenta con tutoriales específicos a continuación.

---

## 👤 Usuarios: primeras transacciones

### Crear una cuenta local

```bash
pltd keys add mi-cuenta
```

Guarda la frase mnemónica en un lugar seguro: es la llave maestra de tu identidad.

### Consultar el balance

```bash
pltd q bank balances $(pltd keys show mi-cuenta -a)
```

### Enviar valor

```bash
pltd tx bank send mi-cuenta <direccion_destino> 100000uplt \
  --fees 500uplt \
  --chain-id plt-test0 \
  --node http://127.0.0.1:26657 \
  --yes
```

> ✉️ Usa unidades `uplt` (micro-PLT). 1 PLT = 1,000,000 uplt.

---

## 🧱 Nodos: desplegar y sincronizar

### Inicializar configuración

```bash
pltd init bootstrap --chain-id plt-test0
```

Este comando crea `~/.plt/config/` con los archivos base.

### Configurar parámetros esenciales

Edita `~/.plt/config/app.toml` y establece:

```toml
minimum-gas-prices = "0.001uplt"
```

En `~/.plt/config/config.toml`, ajusta:

```toml
seeds = ""
persistent_peers = "<peer_id>@<ip>:26656"
```

### Sincronizar con la red

```bash
pltd start
```

Monitorea los logs para verificar conexiones P2P y progreso de bloques.

### Monitoreo y diagnósticos

```bash
# Estado general del nodo
curl http://127.0.0.1:26657/status

# Altura del bloque más reciente
curl -s http://127.0.0.1:26657/block | jq '.result.block.header.height'

# Información del nodo en la red
env PATH="$HOME/go/bin:$PATH" pltd tendermint show-node-id
```

> 📡 Para exponer un nodo público, abre los puertos `26656`, `26657`, `1317`, `9090` y configura `external_address` en `config.toml`.

---

## ⚒️ Validadores: asegurar el consenso

### Crear una cuenta de validador

```bash
pltd keys add validador
```

### Financiar la cuenta

```bash
pltd genesis add-genesis-account validador 100000000uplt
```

### Generar la transacción de autodelegación

```bash
pltd genesis gentx validador 1000000uplt \
  --chain-id plt-test0 \
  --commission-rate 0.10 \
  --commission-max-rate 0.20 \
  --commission-max-change-rate 0.01
```

### Incluir la transacción en el génesis (red local)

```bash
pltd genesis collect-gentxs
pltd genesis validate-genesis
```

### Enviar una transacción de validador en red activa

```bash
pltd tx staking create-validator \
  --amount 1000000uplt \
  --from validador \
  --moniker "mi-validador" \
  --pubkey $(pltd tendermint show-validator) \
  --chain-id plt-test0 \
  --commission-rate 0.10 \
  --min-self-delegation 1 \
  --fees 5000uplt \
  --yes
```

### Pausar validación o hacer unbonding

```bash
# Dejar de validar temporalmente
pltd tx slashing unjail --from validador --chain-id plt-test0 --fees 5000uplt --yes

# Retirar delegaciones gradualmente (21 días de unbonding por defecto)
pltd tx staking unbond $(pltd keys show validador -a) 500000uplt \
  --from validador \
  --chain-id plt-test0 \
  --fees 5000uplt \
  --yes
```

> 🛡️ Mantén infraestructura redundante, monitoreo activo y políticas de seguridad física y lógica.

---

## 🧠 Desarrolladores: construir sobre PLT

### Endpoints clave

- **gRPC**: `localhost:9090`
- **REST API**: `http://127.0.0.1:1317`
- **WebSocket RPC**: `ws://127.0.0.1:26657/websocket`

### Consultas desde gRPC

```bash
grpcurl -plaintext localhost:9090 cosmos.bank.v1beta1.Query/AllBalances \
  -d '{"address":"<direccion>"}'
```

### REST para transacciones y estado

```bash
curl -s "http://127.0.0.1:1317/cosmos/bank/v1beta1/balances/<direccion>" | jq
```

### Crear módulos personalizados

1. Clona `pltnet` y habilita un nuevo módulo en `app/app.go`.
2. Define mensajes, tipos y keeper en `x/<modulo>/`.
3. Registra las rutas en `app/app.go` y actualiza `cmd/pltd/root.go` si añades CLI.
4. Escribe pruebas en `x/<modulo>/keeper/` y `x/<modulo>/module_test.go`.

> 🧪 Usa `make test` y `go test ./...` para validar la lógica antes de desplegar.

---

## 🪙 Economía de PLT

- **Oferta total fija**: emisión inicial determinada por génesis, con inflación programada.
- **Gas**: las tarifas se calculan en `uplt`, con precios mínimos configurables por cada nodo.
- **Recompensas decrecientes**: los incentivos por bloque se reducen en el tiempo, privilegiando a validadores que mantienen disponibilidad sostenida.

---

## 📦 Estructura del repositorio

- `app/`: configuración de la aplicación Cosmos SDK y módulos activos.
- `cmd/pltd/`: entrada del binario, comandos CLI.
- `proto/`: definiciones Protobuf para módulos personalizados.
- `x/`: módulos específicos de PLT, incluyendo lógica de negocio y keepers.
- `docs/`: documentación complementaria y especificaciones.
- `testutil/`: utilidades para pruebas y escenarios de integración.

---

## 🌐 Red pública de PLT

- **Chain ID de referencia**: `plt-test0` (testnet soberana).
- **Puertos estándar**: `26656` (P2P), `26657` (RPC), `1317` (REST), `9090` (gRPC).
- **Exploradores comunitarios**: contribuciones bienvenidas, comparte tus enlaces en los canales oficiales.

> 📣 Para participar en los lanzamientos mainnet, únete a los grupos de coordinación y recibe alertas sobre actualizaciones críticas de red.

---

## 📚 Referencias

- [Documentación oficial de Cosmos SDK](https://docs.cosmos.network)
- [Guía de CometBFT](https://docs.cometbft.com)
- [Ignite CLI](https://docs.ignite.com)
- [Repositorio PLT Blockchain](https://github.com/nobelaar/pltnet)
- Comunidad: [Grupo de Telegram](https://t.me/+Rj6VWw-GdasyNzEx), [Canal de Telegram](https://t.me/pltnetwork)

---

## ⚡ Manifiesto PLT

> Somos la red que rehúsa delegar su destino. PLT es el pulso donde el valor humano recupera su dignidad digital. Construimos herramientas, no cadenas; compartimos protocolos, no permisos. Cada bloque es una declaración de independencia: el poder pertenece a quienes lo sostienen, la libertad a quienes transaccionan, la tecnología a quienes la dominan. Únete, valida, desarrolla. Hagamos del valor un derecho soberano.

---

## 🤝 Contribuye

1. Haz un fork del repositorio.
2. Crea una rama descriptiva (`git checkout -b feat/nueva-funcionalidad`).
3. Aporta código, documentación o infraestructura.
4. Envía un Pull Request siguiendo las guías de estilo.

La revolución del valor se construye colaborando.

