# Lunas amarillas — prototipo de experiencia audiovisual para lectura en vivo

Una sola página (`index.html`) con diecisiete escenas a pantalla completa dibujadas con código.
No necesita internet, ni instalación, ni servidor: abre `index.html` en Chrome, Edge o Firefox.

## Controles durante el performance

| Tecla | Acción |
|---|---|
| `→` `↓` `Espacio` `Av Pág` `Enter` | Siguiente escena (los clickers de presentación funcionan) |
| `←` `↑` `Re Pág` `Retroceso` | Escena anterior |
| `1`–`9`, `0` | Saltar a la escena 1–9 y 10 |
| `Mayús`+`1`…`7` | Saltar a las escenas 11–17 |
| `B` o `.` | Fundido a negro / volver (para los silencios) |
| `W` | Mostrar u ocultar la palabra suelta de la escena |
| `F` | Pantalla completa |
| `R` | Modo ensayo: muestra el nombre de la escena arriba a la izquierda |
| `H` | Mostrar u ocultar la ayuda |

Con el ratón: clic en el tercio izquierdo retrocede, en el resto avanza. En pantalla táctil, desliza.
Al mover el ratón aparece, 2 segundos, una barra mínima abajo con puntos para saltar de escena.
Se puede abrir directo en una escena con `index.html#7`.

## Pulsos (el momento exacto de la revelación)

Las escenas 14, 16 y 17 se avanzan por **pulsos** internos: cada `→` pasa al siguiente pulso de la misma escena antes de cambiar a la siguiente (indicado con puntos •◦ junto al contador). `←` retrocede pulso a pulso.

- **Escena 14** (2 pulsos): 1) las criaturas se acercan; 2) la cuerda se tensa y él se eleva.
- **Escena 16** (4 pulsos): 1) repetición idéntica de la escena 11; 2) la escena sigue y pierde calidez; 3) el camino, el hombre que lo sigue; 4) el lugar apartado: la caída de la bolsa, la mano inmóvil.
- **Escena 17** (2 pulsos): 1) la imagen fija con la moneda que rueda; 2) fundido lento a negro. La última imagen queda en pantalla hasta que tú decidas pulsar `→` (o `B` para negro inmediato).

La escena 16, en su primer pulso, es idéntica pixel a pixel a la escena 11: misma mesa, mismas manos, misma luz. El detalle de la figura tras el cristal en la 11 es casi imperceptible; en la 16 se vuelve visible.

Las escenas 5, 9, 11 y 16 entran con un fundido a negro (pausa para el silencio del narrador). El resto usa fundido encadenado lento.

## Sustituir el dibujo por tus videos o imágenes

1. Crea una carpeta `media/` junto a `index.html`.
2. Guarda ahí `scene-01.mp4` … `scene-17.mp4` (video en bucle, sin audio) y/o `scene-01.jpg` … `scene-17.jpg`.
3. Listo: la escena usa tu archivo. Si falta alguno, esa escena conserva el dibujo de código.

En el bloque `CONFIG` (al inicio del `<script>`) puedes ajustar por escena:

- `video` / `image`: ruta propia, o `false` para desactivar.
- `keepProcedural: true` + `mediaBlend: 'screen'` (o `'multiply'`, `'overlay'`): tu video se mezcla sobre el dibujo en vez de reemplazarlo.
- `mediaOpacity`: 0 a 1.
- `word`, `wordPos` (`'center'` o `'low'`), `wordAt` (segundos para que la palabra aparezca sola).
- `enter`: `'cross'` o `'dip'`.

Cambios globales: `fadeMs`, `dipMs`, `grain`, `renderWidth`.

## Rendimiento y proyección

- Para un proyector grande, sube `renderWidth` a `1920`. Si el equipo se queda corto, baja solo (`adaptive: true`).
- Prueba en el mismo equipo y salón que usarás. El grano, el polvo y las llamas se calculan en vivo.
- Las tipografías (Cormorant Garamond y Jost) se piden a Google Fonts. Sin internet se usa Georgia y Arial. Para que se vean igual offline, descarga ambas familias y añade `@font-face` en el `<style>`.

## Estructura del código

- Bloque `SCENES`: cada escena es `{ init(S), draw(ctx, t, dt, S) }` sobre un lienzo de 1280×720. `t` son los segundos desde que entró la escena.
- Bloque `MOTOR`: fundidos, grano, teclado, carga de medios.
- Para añadir una escena: agrega un objeto a `SCENES` y una entrada en `CONFIG.scenes`.

## Qué no incluye

Sonido. La pieza está pensada para acompañar tu voz; si más adelante quieres ambiente sonoro, se puede añadir como capa aparte.
