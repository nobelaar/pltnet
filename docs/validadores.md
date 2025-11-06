# Guía de validadores PLT

## Crear una cuenta de validador

```bash
pltd keys add validador
```

## Financiar la cuenta

```bash
pltd genesis add-genesis-account validador 100000000uplt
```

## Generar la transacción de autodelegación

```bash
pltd genesis gentx validador 1000000uplt \
  --chain-id plt-test0 \
  --commission-rate 0.10 \
  --commission-max-rate 0.20 \
  --commission-max-change-rate 0.01
```

## Incluir la transacción en el génesis (red local)

```bash
pltd genesis collect-gentxs
pltd genesis validate-genesis
```

## Enviar una transacción de validador en red activa

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

## Pausar validación o hacer unbonding

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
