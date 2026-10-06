# Esquema: Hola Mundo en HTML

Documento de referencia con la estructura mínima de una página HTML que muestra "Hola Mundo".

## Estructura del documento

```text
<!DOCTYPE html>
└── <html lang="...">
    ├── <head>
    │   ├── <meta charset="UTF-8">
    │   ├── <meta name="viewport" ...>
    │   └── <title> ... </title>
    └── <body>
        └── <h1> Hola Mundo </h1>
```

## Piezas obligatorias

| Elemento | Rol |
|----------|-----|
| `<!DOCTYPE html>` | Indica HTML5 al navegador |
| `<html>` | Raíz del documento |
| `<head>` | Metadatos (no visibles en la página) |
| `<body>` | Contenido visible |
| `<h1>` | Título principal con el mensaje |

## Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hola Mundo</title>
</head>
<body>
  <h1>Hola Mundo</h1>
</body>
</html>
```

## Flujo de renderizado

1. El navegador lee `<!DOCTYPE html>` y entra en modo estándar.
2. Parsea `<head>` y aplica título y codificación (`UTF-8`).
3. Renderiza el contenido de `<body>`: el encabezado **Hola Mundo**.

## Variantes opcionales

- **Párrafo:** sustituir o acompañar `<h1>` con `<p>Hola Mundo</p>`.
- **Estilo inline:** `<h1 style="color: navy;">Hola Mundo</h1>`.
- **Comentario:** `<!-- Mi primera página -->` antes de `<body>`.
