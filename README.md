# INSIDER — web multijugador

## Puesta en marcha
1. Crea un proyecto en https://supabase.com/ .
2. Abre SQL Editor, pega todo `setup.sql` y pulsa Run (una sola vez, en un proyecto nuevo).
3. En los ajustes/API del proyecto copia Project URL y la clave pública publishable o anon. Edita `config.js` con ambas. Nunca uses la clave secret o service_role.
4. Sube `index.html`, `style.css`, `app.js`, `config.js` a la raíz de un repositorio GitHub. Settings > Pages > Deploy from a branch > main > / (root). Abre la URL publicada.
5. Crea una sala, comparte el enlace y entra desde otros móviles. El anfitrión reparte roles cuando haya cuatro jugadores. Todos pulsan Estoy preparado y empieza la cuenta atrás compartida. Solo el Master puede confirmar el acierto.

## Personalización
- Colores y tipografía: style.css.
- Palabras: array `words` en setup.sql (Faro, Submarino, Brújula, Volcán, Teleférico, Paraguas). Para cambiarlo después, vuelve a ejecutar únicamente la definición CREATE OR REPLACE FUNCTION.
- Reglas: diálogo de index.html.

## Diseño técnico y limitaciones
GitHub Pages aloja la interfaz; Supabase guarda las salas y asigna los roles en el servidor. Las tablas no se pueden leer directamente con la clave pública. La función devuelve solo el rol y la palabra autorizados para el token privado del dispositivo. El enlace contiene el código de sala, no el token. Se consulta el estado cada 1,2 segundos; el límite de tiempo se comprueba en el servidor. El token se conserva al recargar la misma pestaña, pero si se cierra puede perderse. No hay expulsión de jugadores, recuperación de anfitrión, limpieza automática de salas ni protección avanzada contra abuso; recomendado para partidas privadas. La palabra se elige aleatoriamente y puede repetirse entre rondas. No se ha probado contra un proyecto Supabase real. Antes de publicar, prueba con cuatro móviles y verifica el flujo completo. Las votaciones se hacen presencialmente. Proyecto fan no oficial.

## Banco de palabras
Incluye 240 palabras únicas. Si ya ejecutaste setup.sql, ejecuta únicamente actualizar_palabras.sql en Supabase. palabras.txt es una copia de consulta; el banco activo está en la función SQL.
