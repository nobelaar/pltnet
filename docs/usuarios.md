# Guía de usuarios de PLT

## Crear una cuenta local

```bash
pltd keys add mi-cuenta
```

Guarda la frase mnemónica en un lugar seguro: es la llave maestra de tu identidad.

## Consultar el balance

```bash
pltd q bank balances $(pltd keys show mi-cuenta -a)
```

## Enviar valor

```bash
pltd tx bank send mi-cuenta <direccion_destino> 100000uplt \
  --fees 500uplt \
  --chain-id plt-test0 \
  --node http://127.0.0.1:26657 \
  --yes
```

> ✉️ Usa unidades `uplt` (micro-PLT). 1 PLT = 1,000,000 uplt.
