# ¿Combina?

App de bolsillo para decidir a la mañana qué colores de ropa combinan.
Elegís la prenda que ya tenés puesta y a dónde vas, y te muestra seis formas de completar
el outfit — más los colores que conviene evitar con esa base.

Es **un solo archivo** (`index.html`): sin build, sin dependencias, sin conexión a ningún servicio.

## Cómo usarla

1. **¿A dónde vas?** — Oficina · Elegante · Informal
2. **Clima de hoy** — Calor · Templado · Frío (viene preseleccionado según el mes, hemisferio sur)
3. **Ya tengo puesto…** — Arriba · Pantalón · Zapatos, y tocás el color
4. Aparecen las combinaciones ordenadas de mejor a peor, con el motivo de por qué funcionan

En la pestaña **Mi paleta** hay un test de cuatro preguntas (piel, sol, pelo, ojos) que define tu
estación personal: Primavera, Verano, Otoño o Invierno. A partir de ahí las combinaciones que
caen dentro de tu paleta suben en el ranking y llevan la estrella ★.

Todo queda guardado en el celular (`localStorage`). No se envía nada a ningún lado.

## Publicar en GitHub Pages

1. Mergear esta rama a `main`
2. **Settings → Pages → Build and deployment → Deploy from a branch**
3. Branch: `main`, carpeta `/ (root)` → **Save**
4. Un minuto después queda en `https://drotondi.github.io/ColourPallette/`

### En el iPhone

Abrir esa URL en Safari → botón **Compartir** → **Añadir a pantalla de inicio**.
Queda con ícono propio y se abre a pantalla completa, sin barra de Safari.
Respeta el modo oscuro del sistema y las zonas seguras del notch / Dynamic Island.

## Cómo funciona por dentro

Todo vive en `index.html`, en secciones numeradas dentro del `<script>`:

| Sección | Qué hay |
|---|---|
| 1. Datos | `COLORES` — catálogo de 32 colores con hex, temperatura, si es neutro, estaciones y clima |
| 2. Datos | `OCASIONES` — qué colores son admisibles en cada prenda según a dónde vas |
| 3. Motor | `conflictoPar`, `evaluar`, `sugerir` — descartes duros y puntaje |
| 4. Test | `PREGUNTAS` y `calcularEstacion` |
| 5. Estado | persistencia en `localStorage` |
| 6. UI | render de las tres pantallas |

No hay outfits precargados: las combinaciones se **generan y puntúan** en el momento
(~1.500 candidatas por consulta, filtradas a las 6 mejores con variedad forzada).

### Reglas que descartan un outfit

- Negro con marrón
- Negro con azul marino (salvo en informal)
- Zapato negro con pantalón claro o marrón, fuera de lo informal
- Arriba y pantalón casi con la misma claridad — el clásico "azul medio con gris medio"
- Dos colores casi idénticos pero no iguales
- Más de un color saturado peleando por la atención

### Reglas que suman puntos

Dos neutros y un solo acento (60-30-10), contraste marcado entre arriba y abajo, matices
vecinos u opuestos en la rueda de color, coherencia de temperatura cálido/frío, coincidencia
con tu paleta personal y con el clima del día, y un empujón fijo a los clásicos de sastrería
(marino + blanco + marrón, gris + blanco + negro, oliva + crema + camel, etc.).

### Agregar un color

Sumá una entrada a `COLORES` (el HSL y la luminancia se calculan solos desde el hex) y
agregá su `id` a las listas de `OCASIONES` donde corresponda. Nada más.

## Fuentes

- [The VOU — 4 main colour palettes in men's fashion](https://thevou.com/blog/4-main-colour-palettes-mens-fashion/)
- [The VOU — Seasonal colour analysis for men](https://thevou.com/blog/seasonal-colour-analysis-men-guide-find-your-colour-season/)
- [Color Analysis App — Best clothing color palettes for men](https://color-analysis.app/blog/best-clothing-color-palettes-for-men)
- [Gentleman Within — How to mix & match clothing colors for men](https://www.gentlemanwithin.com/how-to-mix-and-match-clothing-colors-for-men/)
