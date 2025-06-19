<h1>Music_Wars</h1>
<p>
<h2>Por: Saul Escola García - Asignatura: Visualización de Datos</h2>
<p>
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
                        El conjunto de datos fundamental para este proyecto es el <a href="https://www.kaggle.com/datasets/jfreyberg/spotify-chart-data" target="_blank">"Spotify Chart Data"</a>, publicado por Jan Freyberg en Kaggle. Este dataset público recopila información de los charts diarios de Spotify a nivel global y para múltiples países. Para este análisis, se ha utilizado una versión que abarca desde principios de 2013 hasta finales de 2022/principios de 2023 (según la última fecha completa disponible en los datos).
                    </p>
                    <p>
                        Para preparar los datos para la visualización del "Bar Chart Race", se realizaron varios pasos de preprocesamiento y transformación utilizando Python y Pandas, almacenados en el archivo <code>df_final_preprocesado.csv</code>, que luego se procesó para generar <code>spotify_data_for_livingcharts_millions_date_1stream_start.csv</code> para la herramienta de visualización online. Los pasos clave incluyeron:
                    </p>
                    <ul>
                        <li><strong>Limpieza de Datos:</strong> Se manejaron valores nulos (especialmente en nombres de canciones) y se aseguró la correcta interpretación de las fechas.</li>
                        <li><strong>Creación de Identificadores de Canción:</strong> Se generó un nombre de visualización único y limpio para cada canción, combinando el título y el artista principal.</li>
                        <li><strong>Agregación Global y Mensual:</strong> Los streams diarios de cada canción en todos los países del dataset original (<code>charts.csv</code>) fueron sumados para obtener un total global diario. Posteriormente, estos totales diarios se agregaron para obtener los streams totales globales por mes para cada canción.</li>
                        <li><strong>Ajuste Inicial de Streams:</strong> Para una mejor visualización en el "race", a las canciones que tenían 0 streams en el primer período se les asignó un valor nominal de 1 stream.</li>
                        <li><strong>Cálculo de Streams Acumulativos:</strong> Se calcularon los streams acumulativos mensuales para cada canción.</li>
                        <li><strong>Conversión a Millones:</strong> Los valores de streams acumulativos se dividieron por un millón para facilitar su lectura en los ejes del gráfico.</li>
                        <li><strong>Optimización:</strong> Se seleccionaron las 200 canciones con mayor número de streams acumulados al final del período para enfocar la visualización.</li>
                    </ul>

<h3>Análisis Exploratorio de Datos (EDA)</h3>
                    <p>
                        El Análisis Exploratorio de Datos (EDA) fue fundamental para comprender la estructura, distribución y tendencias inherentes al dataset, y para guiar las decisiones de la visualización final. A continuación, se presentan los hallazgos más relevantes:
                    </p>

<div style="text-align:center; margin-bottom:25px;">
                        <img src="eda_plots/distribucion_streams.png" alt="Distribución de Streams" style="max-width:80%; border:1px solid #ccc;">
                        <p><em>Figura 1: Distribución de streams por entrada en chart. La escala logarítmica en el eje X evidencia la alta concentración de canciones con streams moderados y la larga cola de "mega-hits" con reproducciones masivas.</em></p>
</div>
<div style="text-align:center; margin-bottom:25px;">
                        <img src="eda_plots/distribucion_posiciones.png" alt="Distribución de Posiciones" style="max-width:80%; border:1px solid #ccc;">
                        <p><em>Figura 2: Distribución de las posiciones ocupadas en los charts. La mayoría de las entradas se concentran en las posiciones del Top 200, como es de esperar.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/distribucion_duracion.png" alt="Distribución de Duración de Canciones" style="max-width:80%; border:1px solid #ccc;">
    <p><em>Figura 3: Distribución de la duración de las canciones (en minutos). Se observa un pico claro alrededor de los 3-4 minutos, típico de las canciones populares.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/proporcion_explicit.png" alt="Proporción de Canciones Explícitas" style="max-width:50%; border:1px solid #ccc;">
    <p><em>Figura 4: Proporción de canciones marcadas como "explícitas" frente a las no explícitas en el dataset.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/top_paises_entradas.png" alt="Top Países por Entradas en Charts" style="max-width:80%; border:1px solid #ccc;">
    <p><em>Figura 5: Top 15 países con mayor número de entradas en los charts, indicando una alta actividad de reporte o escucha en estas regiones.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/top_artistas_apariciones.png" alt="Top Artistas por Apariciones" style="max-width:80%; border:1px solid #ccc;">
    <p><em>Figura 6: Top 15 artistas con más apariciones en los charts globales, destacando a los más consistentemente populares.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/top_generos_apariciones.png" alt="Top Géneros por Apariciones" style="max-width:80%; border:1px solid #ccc;">
    <p><em>Figura 7: Top 20 géneros (según la API de Spotify) por apariciones. La granularidad de los géneros resalta la necesidad de una normalización para análisis de "familias de géneros".</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/evolucion_streams_mensuales.png" alt="Evolución de Streams Totales Mensuales" style="max-width:90%; border:1px solid #ccc;">
    <p><em>Figura 8: Evolución de los streams totales globales agregados mensualmente. Se observa una tendencia general al alza en la actividad de streaming a lo largo de los años. La caída al final corresponde a la completitud de los datos del último año.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/canciones_unicas_mensuales.png" alt="Número de Canciones Únicas Mensuales" style="max-width:90%; border:1px solid #ccc;">
    <p><em>Figura 9: Número de canciones únicas que aparecen en los charts cada mes. Esta métrica también muestra un crecimiento, sugiriendo una mayor rotación o diversidad musical con el tiempo.</em></p>
</div>

<div style="text-align:center; margin-bottom:25px;">
    <img src="eda_plots/top_canciones_streams_acumulados.png" alt="Top Canciones por Streams Acumulados" style="max-width:80%; border:1px solid #ccc;">
    <p><em>Figura 10: Top 20 canciones por streams totales acumulados a lo largo de todo el período. Este gráfico justifica el uso de streams acumulativos para el bar chart race, ya que resalta la popularidad sostenida.</em></p>
</div>

<p>
    Estos análisis exploratorios fueron cruciales para definir la métrica de streams acumulativos como la más idónea para el Bar Chart Race, permitiendo visualizar de forma clara la persistencia y el impacto a largo plazo de las canciones en el competitivo mundo del streaming musical.
</p>
</div>


<h2>3. Visualización Principal: Bar Chart Race de Popularidad Musical</h2>
<p>
    Para responder a las preguntas sobre la evolución de la popularidad de las canciones y la dinámica de los charts, la visualización principal escogida es un <strong>Bar Chart Race</strong>. Esta técnica es particularmente efectiva para mostrar cómo los rankings y las magnitudes cambian a lo largo de una dimensión temporal (en este caso, mes a mes).
</p>
<p>
    La siguiente animación visualiza las <strong>Top 15 canciones</strong> (de un total de 200 canciones más populares globalmente seleccionadas) basadas en sus <strong>streams acumulativos mensuales globales</strong>, desde Abril de 2013 hasta Diciembre de 2022.
</p>

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
    <video controls width="100%" style="max-width: 800px; border: 1px solid #ccc;">
        <source src="Music_Wars.mp4" type="video/mp4"> <!-- ▲▲▲ CAMBIA ESTE NOMBRE DE ARCHIVO ▲▲▲ -->
        Tu navegador no soporta el tag de video. Por favor, considera actualizarlo.
    </video>
</div>

<h3>Justificación de la Elección y Codificaciones Visuales</h3>
<p>
    Un Bar Chart Race fue seleccionado por su capacidad para:
</p>
<ul>
    <li><strong>Mostrar Dinámicas de Ranking:</strong> Permite observar fácilmente qué canciones suben, bajan o se mantienen estables en el top de popularidad.</li>
    <li><strong>Visualizar Magnitudes Comparativas:</strong> La longitud de las barras ofrece una comparación directa de los streams acumulados entre canciones.</li>
    <li><strong>Contar una Historia Temporal:</strong> La animación a través de los meses revela tendencias, la longevidad de los éxitos y la aparición de nuevos fenómenos.</li>
</ul>
<p>
    Las <strong>codificaciones visuales</strong> empleadas y su justificación son las siguientes:
</p>
<dl>
    <dt><strong>Longitud de Barra (Canal de Longitud):</strong></dt>
    <dd>Representa la cantidad total de streams acumulados por cada canción hasta el mes mostrado. Este es un canal visual muy efectivo y preciso para datos cuantitativos, permitiendo comparaciones directas de magnitud.</dd>

<dt><strong>Posición Vertical de la Barra (Canal de Posición):</strong></dt>
<dd>Indica el ranking de la canción en ese mes específico, ordenado de mayor a menor cantidad de streams acumulados. La posición es un canal muy potente para comunicar orden y jerarquía.</dd>

<dt><strong>Etiquetas de Categoría (Nombres de Canción y Artista):</strong></dt>
<dd>Se muestran junto a cada barra (en el eje Y). Utilizan el canal de identidad para nombrar cada barra, permitiendo al espectador identificar qué canción representa cada barra. La fuente y tamaño se han elegido para maximizar la legibilidad.</dd>

<dt><strong>Etiquetas de Valor (Streams Acumulados en Millones):</strong></dt>
<dd>Aparecen al final de cada barra, mostrando el valor numérico exacto de los streams acumulados (en millones). Esto añade precisión cuantitativa a la longitud de la barra.</dd>

<dt><strong>Color de Barra (Canal de Color - Tono):</strong></dt>
<dd>Se utiliza un esquema de colores categórico (ej. 'Paired' o 'tab20') para asignar un color distinto a cada una de las Top 15 canciones. Esto ayuda a distinguir y seguir canciones individuales a medida que cambian de posición en la animación, mejorando la trazabilidad.</dd>

<dt><strong>Animación (Progresión Temporal):</strong></dt>
<dd>El paso de un frame a otro representa el cambio de un mes al siguiente. La interpolación entre frames suaviza las transiciones, haciendo que la "carrera" sea más fluida y fácil de seguir. La etiqueta de período (ej. "Enero - 2015") indica claramente el momento temporal que se está visualizando.</dd>
</dl>
<p>
    La combinación de estas codificaciones busca ofrecer una representación expresiva y efectiva de la evolución de la popularidad musical, permitiendo al usuario identificar patrones, canciones dominantes y la dinámica general del mercado de streaming de Spotify.
</p>


<h2>4. Elementos Interactivos y de Exploración</h2>
<p>
    La principal técnica utilizada para facilitar la exploración de los datos y el descubrimiento de tendencias es la <strong>animación temporal</strong> inherente al Bar Chart Race. Esta animación transforma un conjunto de datos estático y multidimensional en una narrativa visual dinámica.
</p>
<p>
    Aunque la visualización final se presenta como un archivo de video (MP4), lo que limita la interactividad directa con los elementos del gráfico en tiempo real, se proporcionan los siguientes mecanismos que permiten al usuario manipular su experiencia de visualización:
</p>
<ul>
    <li><strong>Controles del Reproductor de Video:</strong>
        <ul>
            <li><strong>Play/Pausa:</strong> Fundamental para que el usuario pueda detener la animación en cualquier punto específico del tiempo (mes/año). Esto permite un análisis más detallado de la configuración del ranking y los valores de streams en un momento particular, facilitando la comparación entre canciones.</li>
            <li><strong>Barra de Progreso (Scrubbing):</strong> Permite al usuario navegar rápidamente hacia adelante o hacia atrás en la línea de tiempo. Esto es útil para revisitar momentos clave, observar transiciones específicas o saltar a períodos de particular interés.</li>
            <li><strong>Control de Velocidad de Reproducción (si el reproductor lo ofrece):</strong> Algunos reproductores permiten acelerar o ralentizar el video, dando al usuario control sobre el ritmo con el que procesa la información.</li>
            <li><strong>Pantalla Completa:</strong> Para una visualización más inmersiva y detallada.</li>
        </ul>
    </li>
</ul>
<p>
    Estas interacciones, aunque básicas, son cruciales para el proceso de exploración y aprendizaje:
</p>
<ul>
    <li><strong>Descubrimiento de Tendencias:</strong> Al pausar y avanzar lentamente, el usuario puede identificar con mayor precisión cuándo una canción comienza su ascenso, cuándo alcanza su pico, y cuánto tiempo permanece en el top, revelando la longevidad de los éxitos.</li>
    <li><strong>Identificación de Patrones:</strong> La capacidad de revisitar secciones permite comparar diferentes épocas o la entrada de nuevos géneros o artistas que marcan un cambio.</li>
    <li><strong>Incentivo a la Exploración:</strong> La naturaleza dinámica del "race" es inherentemente atractiva y anima al usuario a observar los cambios, generando curiosidad sobre "quién ganará" o "qué pasará después".</li>
</ul>
<p>
    <strong>Consideraciones de Implementación y Usabilidad:</strong>
</p>
<ul>
    <li>La elección de un formato de video MP4 asegura una amplia compatibilidad y un buen rendimiento de reproducción en la mayoría de los dispositivos y navegadores.</li>
    <li>La velocidad de la animación (`steps_per_period` en la generación) se ha ajustado para intentar ofrecer un equilibrio entre fluidez y la capacidad de seguir los cambios sin que sea abrumadoramente rápido o excesivamente lento.</li>
    <li>Si esta visualización se implementara directamente en una plataforma web interactiva, se podrían añadir interacciones más ricas, como tooltips con información detallada al pasar el ratón sobre una barra, filtros dinámicos por artista o género, o la posibilidad de seleccionar una canción para resaltar su trayectoria. Para el alcance de este proyecto, la animación en video con controles de reproducción proporciona un nivel de exploración efectivo.</li>
</ul>


## 5. Composición y Diseño Visual
Se ha buscado una composición limpia...

## Material Complementario
- [Repositorio de GitHub con Código y Datos](https://github.com/TU_USUARIO_GITHUB/NOMBRE_DEL_REPOSITORIO)
- [Dataset CSV Final Utilizado](spotify_data_for_livingcharts_millions_date_1stream_start_TOP200.csv)
