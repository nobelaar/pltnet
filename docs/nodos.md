# Guía de despliegue de nodos PLT

## Inicializar configuración

```bash
pltd init bootstrap --chain-id plt-test0
```

Este comando crea `~/.plt/config/` con los archivos base.

## Configurar parámetros esenciales

Edita `~/.plt/config/app.toml` y establece:

```toml
minimum-gas-prices = "0.001uplt"
```

En `~/.plt/config/config.toml`, ajusta:

```toml
seeds = ""
persistent_peers = "<peer_id>@<ip>:26656"
```

## Sincronizar con la red

```bash
pltd start
```

Monitorea los logs para verificar conexiones P2P y progreso de bloques.

## Monitoreo y diagnósticos

```bash
# Estado general del nodo
curl http://127.0.0.1:26657/status

# Altura del bloque más reciente
curl -s http://127.0.0.1:26657/block | jq '.result.block.header.height'

# Información del nodo en la red
env PATH="$HOME/go/bin:$PATH" pltd tendermint show-node-id
```

> 📡 Para exponer un nodo público, abre los puertos `26656`, `26657`, `1317`, `9090` y configura `external_address` en `config.toml`.
