# 🪙 PLT Network

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Release](https://img.shields.io/badge/release-v0.0.1--beta-orange)](https://github.com/nobelaar/pltnet/releases/tag/v0.0.1-beta)
[![CI](https://github.com/nobelaar/pltnet/actions/workflows/ci.yml/badge.svg)](https://github.com/nobelaar/pltnet/actions/workflows/ci.yml)
[![Go](https://img.shields.io/badge/language-Go-00ADD8.svg)](https://go.dev)

> "Poder para crear, libertad para transaccionar, tecnología al servicio de la gente."

PLT es una blockchain soberana construida sobre Cosmos SDK y el motor de consenso CometBFT. El proyecto busca distribuir el poder de crear valor digital y facilitar transacciones libres respaldadas por tecnología abierta, auditable y comunitaria.

## Tabla de contenidos
- [🌌 Visión](#-visión)
- [⚙️ Requisitos previos](#-requisitos-previos)
- [🚀 Instalación rápida](#-instalación-rápida)
- [🧭 Guía general de participantes](#-guía-general-de-participantes)
- [👤 Usuarios](#-usuarios)
- [🧱 Nodos](#-nodos)
- [⚒️ Validadores](#-validadores)
- [🧠 Desarrolladores](#-desarrolladores)
- [🪙 Economía de PLT](#-economía-de-plt)
- [📦 Estructura del repositorio](#-estructura-del-repositorio)
- [📚 Referencias](#-referencias)
- [⚡ Manifiesto PLT](#-manifiesto-plt)
- [🤝 Contribuye](#-contribuye)
- [🌱 Comunidad](#-comunidad)

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

Cada rol cuenta con tutoriales específicos y guías prácticas detalladas en la carpeta [`docs/`](docs/).

---

## 👤 Usuarios

Guía paso a paso para crear cuentas, consultar balances y enviar transacciones en [docs/usuarios.md](docs/usuarios.md).

---

## 🧱 Nodos

Procedimientos para inicializar nodos, sincronizar con la red y monitorear métricas en [docs/nodos.md](docs/nodos.md).

---

## ⚒️ Validadores

Instrucciones para preparar claves, enviar transacciones de validación y gestionar penalizaciones en [docs/validadores.md](docs/validadores.md).

---

## 🧠 Desarrolladores

Recursos para consumir APIs, extender módulos y ejecutar pruebas en [docs/desarrolladores.md](docs/desarrolladores.md).

---

## 🪙 Economía de PLT

- **Oferta total fija**: emisión inicial determinada por génesis, con inflación programada.
- **Gas**: las tarifas se calculan en `uplt`, con precios mínimos configurables por cada nodo.
- **Recompensas decrecientes**: los incentivos por bloque se reducen en el tiempo, privilegiando a validadores que mantienen disponibilidad sostenida.

---

## 📦 Estructura del repositorio

| Directorio / archivo | Descripción |
| --- | --- |
| `app/` | Configuración de la aplicación Cosmos SDK y módulos habilitados. |
| `cmd/` | Entradas de línea de comandos, incluyendo `pltd`. |
| `proto/` | Definiciones Protobuf para los módulos personalizados de la red. |
| `x/` | Módulos específicos de PLT con lógica de negocio y keepers. |
| `docs/` | Documentación funcional y guías de operación. |
| `testutil/` | Utilidades de pruebas e integración. |
| `Makefile` | Recetas de automatización para desarrollo y CI. |
| `config.yml` | Configuración auxiliar del proyecto. |

---

## 📚 Referencias

- [Documentación oficial de Cosmos SDK](https://docs.cosmos.network)
- [Guía de CometBFT](https://docs.cometbft.com)
- [Ignite CLI](https://docs.ignite.com)
- [Repositorio PLT Blockchain](https://github.com/nobelaar/pltnet)

---

## ⚡ Manifiesto PLT

> Somos la red que rehúsa delegar su destino. PLT es el pulso donde el valor humano recupera su dignidad digital. Construimos herramientas, no cadenas; compartimos protocolos, no permisos. Cada bloque es una declaración de independencia: el poder pertenece a quienes lo sostienen, la libertad a quienes transaccionan, la tecnología a quienes la dominan. Únete, valida, desarrolla. Hagamos del valor un derecho soberano.

---

## 🤝 Contribuye

1. Haz un fork del repositorio.
2. Crea una rama descriptiva (`git checkout -b feat/nueva-funcionalidad`).
3. Aporta código, documentación o infraestructura siguiendo la guía de [CONTRIBUTING.md](CONTRIBUTING.md).
4. Envía un Pull Request verificando las listas de comprobación del repositorio.

### Metadatos del repositorio

- **Descripción sugerida**: "PLT Network — poder para crear, libertad para transaccionar. Blockchain soberana construida con Cosmos SDK y CometBFT."
- **Temas (topics) recomendados**: `cosmos-sdk`, `blockchain`, `tendermint`, `go`, `cryptocurrency`.
- **Documentación pública**: publicar la carpeta [`docs/`](docs/) mediante GitHub Pages o una wiki comunitaria para facilitar el acceso a las guías actualizadas.

---

## 🌱 Comunidad

- [Grupo de Telegram](https://t.me/+Rj6VWw-GdasyNzEx)
- [Canal de Telegram](https://t.me/pltnetwork)

Participa en la conversación, comparte ideas de mejora y ayuda a llevar PLT a producción.
