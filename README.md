# atlantic-city-backend

API REST **simulada** del CRM piloto de Atlantic City, construida con [JSON Server](https://github.com/typicode/json-server).
Proyecto EFSRT · Desarrollo de los Componentes de la Capa de Vista · IDAT 2026-III · Grupo 02.

> En el piloto la lógica de negocio vive en el frontend y esta API solo simula la persistencia.
> La evolución prevista es reemplazarla por **Node.js + Express + MySQL 8** manteniendo los mismos recursos REST,
> de modo que el frontend solo cambie su URL base (ver la arquitectura de la Fase 02 · Actividad 06).

## Requisitos

- Node.js 18 o superior y npm

## Uso

```bash
npm install
npm start          # http://localhost:3001
npm run dev        # igual, con 300 ms de retardo para probar los estados de carga
```

## Recursos

Las colecciones siguen el modelo de datos normalizado de la Fase 02 · Actividad 05 (15 tablas en 3FN).
Los nombres de los campos son los mismos que tendrán las columnas en MySQL.

| Recurso | Tabla (modelo físico) | Uso en el frontend |
|---------|-----------------------|--------------------|
| `/roles`, `/usuarios` | `rol`, `usuario` | Inicio de sesión y menú por rol |
| `/clientes`, `/telefonos`, `/categorias` | `cliente`, `telefono_cliente`, `categoria_cliente` | Registro y gestión de clientes |
| `/visitas`, `/detalles`, `/salas`, `/juegos`, `/preferencias` | `visita`, `detalle_visita_juego`, `sala`, `juego`, `preferencia_cliente` | Visitas y juegos |
| `/segmentos`, `/promociones`, `/participaciones` | `segmento`, `promocion`, `participacion` | Segmentación y promociones |
| `/casos`, `/seguimientos` | `caso_atencion`, `seguimiento_caso` | Atención al cliente |

Ejemplos (JSON Server 0.17):

```http
GET  /clientes?nro_documento=45781236
GET  /clientes?_page=1&_limit=10
GET  /casos?estado=ABIERTO
POST /visitas
PATCH /casos/1
```

## Usuarios de demostración

Todos usan la contraseña `demo123` (datos ficticios, solo para el piloto):

| Usuario | Rol |
|---------|-----|
| `operaciones` | OPERACIONES |
| `marketing` | MARKETING |
| `servicio` | SERVICIO_CLIENTE |
| `gerencia` | GERENCIA |
| `inactivo` | OPERACIONES (cuenta inactiva, para probar el rechazo) |

> **Seguridad:** JSON Server no autentica de verdad y guarda la contraseña en texto plano.
> Es aceptable solo con datos ficticios en el piloto; la autenticación real (contraseñas cifradas y validación en el servidor)
> corresponde a la evolución con Express.
