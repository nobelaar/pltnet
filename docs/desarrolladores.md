# Guía para desarrolladores de PLT

## Endpoints clave

- **gRPC**: `localhost:9090`
- **REST API**: `http://127.0.0.1:1317`
- **WebSocket RPC**: `ws://127.0.0.1:26657/websocket`

## Consultas desde gRPC

```bash
grpcurl -plaintext localhost:9090 cosmos.bank.v1beta1.Query/AllBalances \
  -d '{"address":"<direccion>"}'
```

## REST para transacciones y estado

```bash
curl -s "http://127.0.0.1:1317/cosmos/bank/v1beta1/balances/<direccion>" | jq
```

## Crear módulos personalizados

1. Clona `pltnet` y habilita un nuevo módulo en `app/app.go`.
2. Define mensajes, tipos y keeper en `x/<modulo>/`.
3. Registra las rutas en `app/app.go` y actualiza `cmd/pltd/root.go` si añades CLI.
4. Escribe pruebas en `x/<modulo>/keeper/` y `x/<modulo>/module_test.go`.

> 🧪 Usa `make test` y `go test ./...` para validar la lógica antes de desplegar.
