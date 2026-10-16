# NavBar Intra · Kiub

Barra de navegación de la intranet (`resources/js/components/AppHeader.vue`).
Conserva los colores de la barra original y añade los efectos y el movimiento de
la referencia en video.

## Estructura

- **Módulos en la barra principal**: Servicios KH, HR.Space, Kaizen University,
  Comunicaciones (desplegable con Noticias y Calendario) y Koupons.
- **Lado derecho**: búsqueda, herramientas, notificaciones y tarjeta de usuario.
- **Herramientas**: botón circular con desplegable; cada rol ve solo las suyas.
  En móvil se mueven al menú lateral, en la sección «Administración».

## Efectos

- **Barra de cristal que respira**: se expande al entrar el cursor y vuelve con
  rebote al salir; se mantiene expandida mientras hay un menú o la búsqueda abierta.
- **Brillo que sigue al cursor** en el borde y la superficie de la barra.
- **Enlaces**: el texto sube y crece levemente, un subrayado crece desde la izquierda
  (y se retrae hacia la izquierda), y el chevron de «Comunicaciones» gira.
- **Píldora activa deslizante** con punto pulsante; se mueve al instante al hacer clic,
  incluso entre visitas de Inertia.
- **Búsqueda que se transforma**: el botón circular se estira hasta un campo con `ESC`
  y botón de cierre; la tarjeta de usuario cede espacio mientras está abierta.
- **Herramientas**: la llave gira al pasar el cursor y el menú entra escalonado.
- **Campana** que se balancea al pasar el cursor y contador opcional.
- **Tarjeta de usuario** con ola de letras en el nombre, avatar que gira y menú.
- **Móvil**: panel lateral con entrada escalonada y submenús plegables.
- Respeta `prefers-reduced-motion` y el modo oscuro (`.dark` en `<html>`).

## Uso

```vue
<AppHeader
    :breadcrumbs="breadcrumbs"
    :allowed-tools="page.props.auth.tools"
    user-subtitle="Kaizen Holdings · IT Tecnología"
    :notification-count="3"
    @search="(q) => router.get('/buscar', { q })"
    @notifications="abrirNotificaciones"
/>
```

| Prop | Tipo | Por defecto | Descripción |
| --- | --- | --- | --- |
| `breadcrumbs` | `BreadcrumbItem[]` | `[]` | Igual que antes. |
| `allowedTools` | `string[]` | todas | Claves de herramientas visibles para el rol. `[]` oculta el botón. |
| `userSubtitle` | `string` | email del usuario | Segunda línea de la tarjeta de usuario. |
| `notificationCount` | `number` | `0` | Muestra el contador sobre la campana si es mayor que 0. |
| `animatedMark` | `boolean` | `true` | Barras animadas junto al logo. |

Eventos: `search` (texto buscado al pulsar Enter) y `notifications` (clic en la campana).

### Claves de herramientas

`gestion-servicios`, `data-master`, `nuevo-ingreso`, `movimiento-personal`,
`egreso-personal`, `prestaciones`, `vacaciones`, `permisos`, `beneficios`,
`admin-koupons`, `contratos-laborales`, `asignacion-equipos`, `asignacion-licencias`.

### Rutas por completar

Los `href` de los módulos (`navEntries`) y de las herramientas (`toolCatalog`) son
provisionales (`/servicios-kh`, `/herramientas/vacaciones`, …); cámbialos por tus
rutas de Wayfinder.
