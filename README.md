IRONFLOW MAX — Generador de Rutinas de 60 Minutos Exactos
https://img.shields.io/badge/version-5.0-blue
https://img.shields.io/badge/license-MIT-green
https://img.shields.io/badge/platform-web-lightgrey

IRONFLOW MAX es una herramienta web gratuita para profesores de gimnasio que necesitan generar rutinas de entrenamiento de exactamente 60 minutos para grupos de alumnos avanzados. El sistema lee los ejercicios desde un archivo JSON externo, los organiza según diferentes tipos de split (PPL, Upper/Lower, Full Body) y ajusta automáticamente las series para cumplir el tiempo objetivo.

✨ Características principales
🕒 60 minutos exactos – algoritmo que ajusta series y repeticiones para que cada sesión dure 60 minutos (10′ calentamiento + 45′ trabajo + 5′ vuelta).

📄 Rutinas externas – los ejercicios se definen en rutinas.json, fácil de modificar sin tocar el código HTML.

🎯 Tres tipos de split:

PPL (Push / Pull / Legs) – 5 días/semana.

Upper / Lower – 4 días/semana.

Full Body – 3 días/semana.

🖨️ Impresión en blanco y negro – botón para guardar la rutina como PDF sin elementos decorativos.

📱 Diseño responsive – funciona en ordenadores, tablets y móviles.

🧠 Lógica profesional – respeta principios como prioridad de multiarticulares, RIR 1, descansos diferenciados y tempo controlado.

📁 Estructura de archivos
text
tu_carpeta/
├── ironflow max.html      # Interfaz principal y motor de rutinas
└── rutinas.json           # Archivo con los ejercicios organizados por día
Importante: ambos archivos deben estar en la misma carpeta para que el HTML pueda cargar el JSON correctamente.

🔧 Instalación y configuración
Descarga los dos archivos (ironflow max.html y rutinas.json).

Colócalos en la misma carpeta de tu ordenador o servidor web.

Abre ironflow max.html con cualquier navegador moderno (Chrome, Firefox, Edge, Safari).

Personaliza los ejercicios editando rutinas.json (explicado abajo).

No necesitas instalar nada más, ni conexión a Internet (excepto para las fuentes de Google y los anuncios de AdSense).

📝 Cómo personalizar las rutinas (rutinas.json)
El archivo rutinas.json tiene esta estructura:

json
{
  "Lunes": {
    "enfoque": "Pecho y Tríceps",
    "ejercicios": [
      { "nombre": "Press de Banca con Barra", "musculo": "Pecho", "tipo": "Compuesto" },
      { "nombre": "Press Inclinado con Mancuernas", "musculo": "Pecho", "tipo": "Compuesto" },
      ...
    ]
  },
  "Martes": { ... },
  ...
}
✏️ Reglas para editar:
Días válidos: Lunes, Martes, Miércoles, Jueves, Viernes (con o sin tilde, el script lo normaliza).

Propiedades de cada ejercicio:

nombre – texto libre.

musculo – grupo muscular (se muestra en la tabla).

tipo – debe ser "Compuesto" o "Aislamiento". Esto afecta las series, repeticiones y descansos por defecto.

⚙️ Valores por defecto que asigna el sistema:
Tipo	Series	Rango de repeticiones	Descanso	RIR
Compuesto	3–5	6–10	90 s	RIR 1
Aislamiento	2–3	10–15	60 s	RIR 1–2
El motor luego ajusta las series (aumenta o reduce) para que el tiempo total de trabajo sea exactamente 45 minutos (2700 segundos). El tempo de repetición es fijo: 4 segundos por repetición (2″ excéntrica + 2″ concéntrica).

Puedes modificar los rangos de series o repeticiones directamente en el JSON, o cambiar la lógica en la función convertJSONtoDB() dentro del HTML si lo deseas.

🧠 Explicación de los splits
PPL (Push / Pull / Legs)
Días: LUN (PUSH), MAR (PULL), MIÉ (LEGS), JUE (PUSH), VIE (PULL)

Push: ejercicios de empuje (pecho, hombros, tríceps)

Pull: ejercicios de tracción (espalda, bíceps)

Legs: piernas completas (cuádriceps, isquios, glúteos, gemelos)

Ideal para volumen alto en tren superior.

Upper / Lower
Días: LUN (UPPER), MAR (LOWER), MIÉ (REST), JUE (UPPER), VIE (LOWER)

Upper: pecho, espalda, hombros, bíceps, tríceps.

Lower: piernas completas.

Recomendado para 4 días/semana con buena recuperación.

Full Body
Días: LUN (FULL BODY), MAR (REST), MIÉ (FULL BODY), JUE (REST), VIE (FULL BODY)

Trabaja todo el cuerpo cada sesión.

Perfecto para principiantes o personas con poco tiempo (3 días/semana).

🕹️ Cómo usar la herramienta
Selecciona un turno (ej. 18:00 → 19:00). El sistema lo mostrará en el encabezado de la rutina.

Elige el tipo de split (PPL, Upper/Lower o Full Body).

Haz clic en "GENERAR RUTINA".

Verás los días de la semana en pestañas. Haz clic en cada día para ver su rutina.

Si deseas guardar la rutina del día actual, pulsa "IMPRIMIR / GUARDAR PDF" – se abrirá el diálogo de impresión; elige "Guardar como PDF". El PDF aparecerá en blanco y negro, sin anuncios ni elementos extra.

🧮 ¿Cómo garantiza los 60 minutos exactos?
Calentamiento: 10 minutos fijos.

Vuelta a la calma: 5 minutos fijos.

Trabajo principal: 45 minutos (2700 segundos).

El algoritmo calcula el tiempo de cada ejercicio como:
(series × reps_medias × 4 seg) + ((series - 1) × descanso_en_segundos).

Luego ajusta las series (dentro de los rangos definidos) hasta que el tiempo total se aproxime a 2700 segundos con una tolerancia de ±30 segundos.

El resultado siempre se redondea a 60 minutos exactos en la interfaz.

🖨️ Impresión y PDF
Al hacer clic en el botón de imprimir, se aplican estilos especiales:

Fondo blanco, texto negro.

Se ocultan: cabecera, panel de control, publicidad, FAQs, botones y elementos de navegación.

Solo se imprime la tarjeta de la rutina actual (tabla de ejercicios, tiempos, encabezado del día).

Ideal para entregar a los alumnos en papel o como archivo PDF.

🛠️ Personalización avanzada
Si quieres modificar el comportamiento del motor de tiempo (series, descansos, tempo), edita la función convertJSONtoDB() dentro de <script> en el HTML. Allí encontrarás los valores por defecto:

javascript
const seriesBase = esCompuesto ? 3 : 2;
const rLo = esCompuesto ? 6 : 10;
const rHi = esCompuesto ? 10 : 15;
const rest = esCompuesto ? 90 : 60;
const tRep = 4;  // segundos por repetición
También puedes cambiar el tempo (tRep) o los rangos de series máximas/mínimas en la función adjustTo45Min().

📦 Dependencias externas
Google Fonts – se cargan las fuentes Barlow Condensed, Barlow y Roboto Mono.

Google AdSense – el código está comentado por defecto. Debes insertar tu propio publisher ID si deseas monetizar. Los contenedores de anuncios son meros placeholders.

🤝 Contribuciones
Si deseas mejorar el proyecto, puedes:

Añadir más variantes de split (ej. PPL con doble pierna).

Incorporar un selector de nivel (principiante/intermedio/avanzado) para ajustar los rangos de repeticiones y descansos.

Traducir la interfaz a otros idiomas.

Simplemente modifica el HTML o el JSON y comparte tus cambios.

📄 Licencia
MIT License – libre de usar, modificar y distribuir, tanto para fines personales como comerciales. Agradeceremos una mención al proyecto original si lo redistribuyes.

🙋 Preguntas frecuentes
¿Puedo usar mis propios ejercicios?
Sí, edita rutinas.json siguiendo el formato. El resto lo hace la herramienta automáticamente.

¿Qué pasa si un día no quiero entrenar?
Los splits ya incluyen días de descanso (ej. miércoles en Upper/Lower). Si deseas un split completamente personalizado, puedes modificar el objeto SPLITS en el código JavaScript.

¿Los 60 minutos incluyen el tiempo de explicación del profesor?
La duración está pensada para el trabajo efectivo de los alumnos. El profesor puede añadir instrucciones al inicio o al final fuera de los 60 minutos.

¿Puedo quitar la publicidad?
Sí, elimina o comenta las etiquetas div class="ad-slot" y las referencias a AdSense. El proyecto es completamente funcional sin anuncios.

IRONFLOW MAX – Hecho con ❤️ para profesores de gimnasio que valoran la precisión y la eficiencia.

