<h1>Music_Wars</h1>
<h2>Por: Saul Escola García - Asignatura: Visualización de Datos</h2>

<h2>1. Introducción: Preguntas y Objetivos</h2>
<p>
    La música es una fuerza omnipresente y en constante evolución, y las plataformas de streaming como Spotify se han convertido en el principal barómetro de las tendencias musicales globales. Este proyecto se sumerge en el vasto océano de datos de los charts de Spotify para visualizar y comprender la dinámica de la popularidad de las canciones a lo largo de casi una década.
</p>
<p>
    Partiendo del dataset "Spotify Chart Data" (que abarca desde 2013 hasta finales de 2023), que incluye información sobre millones de entradas en los charts de diversos países, surgieron las siguientes preguntas clave:
</p>
<ul>
    <li>¿Cómo ha evolucionado el ranking de las canciones más escuchadas a nivel global mes a mes?</li>
    <li>¿Qué canciones han logrado un impacto duradero, manteniéndose en la cima de la popularidad durante períodos extensos?</li>
    <li>¿Existen "fenómenos musicales" o "one-hit wonders" claramente identificables por su rápido ascenso y descenso en los charts?</li>
    <li>¿Se pueden observar patrones o cambios en la velocidad con la que nuevas canciones alcanzan el estrellato y otras son desplazadas?</li>
</ul>
<p>
    Los <strong>objetivos principales</strong> de este proyecto de visualización son:
</p>
<ol>
    <li><strong>Presentar de forma dinámica y atractiva</strong> la evolución de la popularidad de las canciones (Top 1000 global) utilizando streams acumulativos mensuales como métrica principal.</li>
    <li><strong>Facilitar la identificación de tendencias</strong>, canciones dominantes y la naturaleza cambiante de los gustos musicales a lo largo del tiempo.</li>
    <li><strong>Demostrar la aplicación de técnicas de preprocesamiento de datos y visualización de información</strong> para extraer insights de un conjunto de datos complejo y de gran volumen.</li>
</ol>
<p>
    A través de un "Bar Chart Race", se busca ofrecer una narrativa visual que no solo muestre datos, sino que también cuente la historia de la música que ha marcado la última década en Spotify.
</p>

<h2>2. El Dataset: Origen, Procesamiento y Análisis Exploratorio</h2>
<p>
    El conjunto de datos fundamental para este proyecto es el <a href="https://www.kaggle.com/datasets/jfreyberg/spotify-chart-data" target="_blank">"Spotify Chart Data"</a>, publicado por Jan Freyberg en Kaggle. Este dataset público recopila información de los charts diarios de Spotify a nivel global y para múltiples países, abarcando en nuestra versión procesada desde principios de 2013 hasta finales de 2023.
</p>
<p>
    Para preparar los datos para la visualización del "Bar Chart Race", se realizaron varios pasos de preprocesamiento y transformación:
</p>
<ul>
    <li><strong>Limpieza de Datos:</strong> Se manejaron valores nulos y se aseguró la correcta interpretación de las fechas.</li>
    <li><strong>Creación de Identificadores de Canción:</strong> Se generó un nombre de visualización único para cada canción combinando el título y el artista principal.</li>
    <li><strong>Agregación Global y Mensual:</strong> Los streams diarios de cada canción en todos los países fueron sumados para obtener un total global diario. Posteriormente, estos totales diarios se agregaron para obtener los streams totales globales por mes para cada canción.</li>
    <li><strong>Cálculo de Streams Acumulativos:</strong> Para la visualización principal, se calcularon los streams acumulativos mensuales. Esto significa que para cada mes, el valor de una canción representa el total de streams que ha acumulado desde su primera aparición en los datos hasta ese mes inclusive. Esta métrica es crucial para mostrar el crecimiento y la popularidad sostenida a lo largo del tiempo.</li>
    <li><strong>Optimización:</strong> Se seleccionaron las 1000 canciones con mayor número de streams acumulados al final del período para enfocar la visualización en las más relevantes.</li>
</ul>

<h3>Análisis Exploratorio de Datos (EDA)</h3>
<p>
    Antes de crear la visualización final, se realizó un Análisis Exploratorio de Datos para comprender mejor la naturaleza y las tendencias inherentes al dataset. A continuación, se presentan algunos de los hallazgos y gráficos más relevantes:
</p>

<!-- 
    INSTRUCCIÓN: Aquí es donde insertarás las imágenes de tus gráficos EDA 
    y una breve descripción para cada uno. Sube las imágenes a tu repositorio de GitHub 
    (quizás en una carpeta 'images') y enlaza a ellas.
    Ejemplos de qué gráficos EDA incluir (basados en lo que generamos):
    - Distribución de Streams (mostrando el sesgo)
    - Evolución de Streams Totales Mensuales (Global)
    - Número de Canciones Únicas en Charts por Mes
    - Top N Artistas por Apariciones o Streams Acumulados Totales
    - Top N Géneros (si hiciste la normalización y quieres incluirlo aquí, aunque la categoría de género se usa más en el race)
-->

<div style="text-align:center; margin-bottom:20px;">
    <img src="ruta/a/tu/grafico_distribucion_streams.png" alt="Distribución de Streams de Canciones" style="max-width:70%; border:1px solid #ccc;">
    <p><em>Figura 1: Distribución de streams por entrada en chart (escala logarítmica). Se observa una clara concentración en valores bajos, con pocas canciones alcanzando streams masivos, lo que justifica el enfoque en un "Top N" para el race.</em></p>
</div>

<div style="text-align:center; margin-bottom:20px;">
    <img src="ruta/a/tu/grafico_streams_totales_mensuales.png" alt="Evolución de Streams Totales Mensuales" style="max-width:70%; border:1px solid #ccc;">
    <p><em>Figura 2: Evolución de los streams totales globales agregados mensualmente. Se aprecia una tendencia general al alza en la actividad de streaming a lo largo de los años, con fluctuaciones estacionales.</em></p>
</div>

<div style="text-align:center; margin-bottom:20px;">
    <img src="ruta/a/tu/grafico_canciones_unicas_mes.png" alt="Número de Canciones Únicas Mensuales" style="max-width:70%; border:1px solid #ccc;">
    <p><em>Figura 3: Número de canciones únicas que aparecen en los charts cada mes. Esta métrica también muestra un crecimiento, sugiriendo una mayor rotación o diversidad musical con el tiempo.</em></p>
</div>

<div style="text-align:center; margin-bottom:20px;">
    <img src="ruta/a/tu/grafico_top_canciones_acumuladas.png" alt="Top Canciones por Streams Acumulados" style="max-width:70%; border:1px solid #ccc;">
    <p><em>Figura 4: Top 20 canciones por streams totales acumulados a lo largo de todo el período. Este gráfico estático da una idea de los "grandes éxitos" generales y justifica el uso de streams acumulativos para el bar chart race, ya que resalta la popularidad sostenida.</em></p>
</div>

<p>
    Estos análisis preliminares ayudaron a confirmar la idoneidad de un Bar Chart Race con streams acumulativos para visualizar la dinámica de la popularidad y a identificar las canciones más significativas para incluir en la animación.
</p>

## 3. Análisis Visual y Elección de Codificaciones
La visualización principal es un **Bar Chart Race**:

<!-- Para incrustar un video, GitHub no lo hace directamente en el README.
     Puedes subir el video al repositorio y poner un enlace de descarga,
     o subirlo a YouTube/Vimeo y poner el enlace.
     Para una imagen (si haces un GIF del race):
     ![Bar Chart Race](spotify_race.gif)
     Si es un MP4, la mejor opción es poner un thumbnail y enlazar al video:
-->
[![Thumbnail del Bar Chart Race](url_del_thumbnail.png)](nombre_de_tu_video.mp4)
*Haz clic en la imagen para ver el video del Bar Chart Race (asegúrate de que `nombre_de_tu_video.mp4` esté en el repositorio).*

**Justificación de las codificaciones visuales:**
- **Longitud de Barra:** ...
- ...

### Análisis Exploratorio de Datos (EDA)
![Gráfico EDA 1](nombre_de_tu_grafico_eda1.png)
*Descripción del gráfico EDA 1...*

![Gráfico EDA 2](nombre_de_tu_grafico_eda2.png)
*Descripción del gráfico EDA 2...*

## 4. Elementos Interactivos
La visualización (el video) ofrece interactividad a través de los controles del reproductor...

## 5. Composición y Diseño Visual
Se ha buscado una composición limpia...

## Material Complementario
- [Repositorio de GitHub con Código y Datos](https://github.com/TU_USUARIO_GITHUB/NOMBRE_DEL_REPOSITORIO)
- [Dataset CSV Final Utilizado](spotify_data_for_livingcharts_millions_date_1stream_start_TOP200.csv)
