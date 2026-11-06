# test-manager-library-3239188-app

Frontend en React de *Manager Library*. Prueba técnica SDD · Ficha ADSO 3239188.

## Papel en el spec

Pantallas de operación para el administrador y el bibliotecario (tarea T-22). Consume el contrato de `api-contract.md` tal cual: no cambia nombres de campos ni rutas.

## Convención de idioma (artículo XI)

Código, componentes y variables en inglés. Textos visibles al usuario en español.

## Pantallas previstas

| Pantalla | Rol | Endpoints que consume | Historia |
|---|---|---|---|
| Login | todos | `POST /auth/login` | HU-01 |
| Catálogo y búsqueda | autenticado | `GET /books`, `GET /categories` | HU-04 |
| Gestión de libros | admin | `POST/PUT/DELETE /books`, portada | HU-03 |
| Socios | admin, bibliotecario | `GET/POST /members` | HU-05 |
| Registrar préstamo | admin, bibliotecario | `POST /loans` | HU-06 |
| Devolver | admin, bibliotecario | `POST /loans/{loan_id}/items/{item_id}/return` | HU-07 |
| Préstamos | admin, bibliotecario | `GET /loans`, `GET /loans/{id}` | HU-08 |
| Vencidos | admin, bibliotecario | `GET /loans/overdue` | HU-09 |
| Reporte de más prestados | admin | `GET /reports/most-borrowed` | HU-10 |

## Manejo de errores

El cuerpo de error es único (`code`, `message`, `details`). La app muestra el `message` en español y reacciona según el estado:

| Estado | Comportamiento |
|---|---|
| 401 | Cierra sesión y vuelve al login |
| 403 | Aviso de permisos insuficientes; el menú oculta lo que el rol no puede usar |
| 409 | Aviso del conflicto (sin ejemplares, ya devuelto, socio con vencidos, libro con préstamos abiertos) |
| 422 | Marca los campos indicados en `details` |

## Reglas que la interfaz respeta

- Un préstamo tiene de 1 a 3 libros, sin repetir.
- El reporte puede mostrar el mismo libro en más de una fila (categoría congelada distinta); es correcto.
- Un libro dado de baja deja de aparecer en el catálogo.
- El token se envía como `Authorization: Bearer`; no se guardan datos personales en él.

## Recorrido de punta a punta

Login → buscar libro → registrar préstamo → devolver una línea → ver el reporte.

## Estado

| Elemento | Estado |
|---|---|
| Diseño de pantallas y manejo de errores | Hecho (este documento) |
| Implementación | Pendiente |

> Este README describe el diseño previsto. No afirma que la implementación exista.