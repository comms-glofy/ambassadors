# Glofy Ambassadors · Conteo de puntos y ranking

Herramienta interna de Comms para contar los puntos del Ambassador Program sin APIs de Meta ni de LinkedIn. Usa lo que se ve en pantalla (listas de likes, reacciones, comentarios y reposts), reconoce a cada colaborador/a, guarda todo en la planilla y genera el ranking listo para Slack.

## Archivos
- `index.html` · la herramienta (single-file, sin build). Va en GitHub Pages de comms-glofy, por ejemplo `comms-glofy/ambassadors`.
- `Code.gs` · backend en Google Apps Script, dentro de la planilla "Conteo de puntos | Glofy Ambassadors".

## Instalación (una sola vez, ~10 minutos)

### 1. Planilla
1. Abrir la planilla > Extensiones > Apps Script.
2. Borrar lo que haya, pegar `Code.gs` y guardar.
3. Recargar la planilla. Aparece el menú **Glofy Ambassadors** > **1. Configurar (primera vez)**. Aceptar los permisos.
4. Se crean las pestañas `Participantes`, `Registro`, `Puntajes` y `Config`. Los puntos actuales de "Hoja 1" se migran como "saldo inicial", así el ranking sigue desde donde está. "Hoja 1" no se modifica.
5. El mensaje final muestra la **clave de acceso** (también en el menú > Ver clave de acceso).

### 2. Publicar el backend
1. En Apps Script: Implementar > Nueva implementación > tipo **Aplicación web**.
2. Ejecutar como: **Yo** · Quién tiene acceso: **Cualquier usuario**. (La clave protege los datos.)
3. Copiar la URL que termina en `/exec`.

### 3. Herramienta
1. Subir `index.html` a un repo de comms-glofy con GitHub Pages activado.
2. Abrir la página > Configuración > pegar URL y clave > **Conectar y cargar datos**.
3. Arrastrar el botón "Glofy · Capturar lista" (pestaña 1, sección "Cómo copiar las listas") a la barra de favoritos de Chrome.

## Uso semanal
1. **Posts de la semana**: por cada post de @glofyco de la semana, "+ Post de Instagram / LinkedIn", pegar el link y las listas. Para cada lista: abrirla en la red, tocar el favorito "Capturar lista", "Copiar y cerrar", pegar en la herramienta.
2. Revisar los detectados: cada uno muestra la línea donde apareció. Destildar si es un falso positivo; usar "+ Sumar a alguien que no se detectó" si falta alguien.
3. **Acciones manuales**: historias etiquetadas, videos de Comms, posteos propios, bonus y propuestas.
4. **Revisar y guardar**: ver el detalle y guardar en Sheets. La pestaña `Puntajes` se actualiza con el mismo formato de siempre.
5. **Ranking**: "Descargar PNG para Slack".

## Controles que evitan errores
- Una persona suma una sola vez por like/reacción/repost en cada post.
- Aviso si un post ya fue contabilizado en otra semana, si está repetido o si su fecha cae fuera de la semana.
- Cada carga queda en `Registro` con semana, post, acción y origen (auto o manual). Cualquier carga se puede deshacer desde "Revisar y guardar".
- Bloqueo de cargas duplicadas del mismo lote.

## Detección de nombres
Se reconoce a cada persona por nombre + apellido (LinkedIn) y por combinaciones tipo `nombreapellido` (Instagram). Si alguien usa un usuario de IG distinto, aparece en "usuarios sin asignar" debajo de la lista de likes: se asigna una vez y queda guardado como alias. También se pueden cargar alias en Configuración > Participantes.

## Periodos
Configuración > "Empezar periodo nuevo" (por ejemplo, cada bimestre de premios) arranca el ranking en cero. El historial completo queda en `Registro`.

## Modo local
Sin conexión a Sheets, la herramienta funciona igual guardando en el navegador y permite descargar un CSV con el formato de la planilla.
