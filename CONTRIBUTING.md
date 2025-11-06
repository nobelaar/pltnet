# Guía de contribución a PLT Network

¡Gracias por tu interés en construir PLT! Sigue estos pasos para colaborar de forma efectiva y mantener una experiencia agradable para toda la comunidad.

## 1. Configura tu entorno

```bash
git clone https://github.com/nobelaar/pltnet.git
cd pltnet
go mod tidy
```

## 2. Crea una rama descriptiva

Trabaja siempre en una rama separada basada en `main`.

```bash
git checkout -b feat/mi-funcionalidad
```

Usa prefijos como `feat/`, `fix/`, `docs/`, `chore/` para indicar el tipo de cambio.

## 3. Ejecuta pruebas y linters

Antes de enviar tu contribución, verifica que el código compila y que las pruebas pasan:

```bash
make test
go test ./...
go fmt ./...
go vet ./...
```

Si añades herramientas adicionales (por ejemplo `golangci-lint`), documenta cómo ejecutarlas en tu Pull Request.

## 4. Escribe código y documentación con estilo

- Sigue las guías de estilo oficiales de Go y evita introducir dependencias innecesarias.
- Mantén funciones y módulos pequeños y fáciles de probar.
- Actualiza o crea documentación en `docs/` cuando añadas nuevas funcionalidades o flujos de trabajo.
- Incluye pruebas unitarias y de integración cuando sea posible.

## 5. Nombra tus commits con claridad

Usa mensajes del tipo:

```
<tipo>: resumen breve
```

donde `<tipo>` puede ser `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, etc. Ejemplo: `feat: add governance module skeleton`.

## 6. Prepara tu Pull Request

1. Revisa que `git status` esté limpio y que todos los cambios relevantes estén incluidos.
2. Actualiza la documentación y el `CHANGELOG.md` cuando corresponda.
3. Describe claramente qué problema resuelves, cómo lo abordaste y provee pasos de prueba manual si aplican.
4. Confirma en la plantilla de PR que los tests pasan y que añadiste documentación.

## 7. Recibe retroalimentación

Sé receptivo a los comentarios del equipo de revisión. Las conversaciones respetuosas y enfocadas en mejorar el proyecto son el corazón de una comunidad sana.

¡Gracias por construir PLT Network! 💫
