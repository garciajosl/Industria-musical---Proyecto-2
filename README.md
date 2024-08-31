# Validación de hipótesis ---Proyecto-2 
# Temas
- Introducción
- Herramientas
- Procesamiento
- Validación de hipótesis
- Conclusiones
- Recomendaciones

# Introducción
En un mundo en el que la industria musical es extremadamente competitiva y está en permanente evolución, la capacidad de tomar decisiones basadas en datos se ha convertido en un activo invaluable. En este contexto, una discográfica se enfrenta al emocionante desafío de lanzar un nuevo artista en el escenario musical global. Afortunadamente, cuenta con una herramienta poderosa en su arsenal: un extenso dataset de Spotify con información sobre las canciones más escuchadas en 2023.
La discográfica planteó una serie de hipótesis sobre qué hace que una canción sea más escuchada. Estas hipótesis incluyen:
- Las canciones con un mayor BPM (Beats Por Minuto) tienen más éxito en términos de cantidad de streams en Spotify.
- Las canciones más populares en el ranking de Spotify también tienen un comportamiento similar en otras plataformas como Deezer.
- La presencia de una canción en un mayor número de playlists se relaciona con un mayor número de streams.
- Los artistas con un mayor número de canciones en Spotify tienen más streams.
- Las características de la canción influyen en el éxito en términos de cantidad de streams en Spotify.

# Herramientas
- Power BI
- BigQuery
- SQL
# Procesamiento
Aqui empecé con importar mis datos a big query para poder iniciar con mi proyecto. Lo primero que hice fue trabajar con Big query con las siguientes consultas para un resultado individual y para un resultado general ya teniendo mis tablas unidas.
```sql
 #Contine 95 valores nulos
SELECT
  COUNT(*)
FROM
  `proyecto-2-hipotesis-426715.Original.info`
  where
  key IS NULL

SELECT
  COUNT(*)
FROM
  `proyecto-2-hipotesis-426715.Original.info`
WHERE
  mode IS NULL

SELECT
  COUNT(*)
FROM
  `proyecto-2-hipotesis-426715.Original.info`
WHERE
  bpm IS NULL
```
```sql
 CREATE OR REPLACE TABLE `proyecto-2-hipotesis-426715.Original.new_table_2` AS
SELECT *
FROM `proyecto-2-hipotesis-426715.Original.new_table_2`
WHERE`competition_track_id` IS NOT NULL;
```
Con estas consultas en BigQuery obtuve en;
# track_technical_info
- key: 95 nulls
# track_in_competition
- in_shazam_charts: 50 nulls
De igual manera hice con los valores duplicados en los cuales solo obtuve 4 valores duplicados, los cuales decidi dejarlos ya que no me generaba diferencia alguna.
```sql
  #existen 4 valores duplicados
SELECT
  track_name,
  artist_s__name,
  COUNT(*) AS Cantidad
FROM
  `proyecto-2-hipotesis-426715.Original.Spotify`
GROUP BY
  track_name,
  artist_s__name
HAVING
  COUNT(*)>1
```
Decidí eliminar valores fuera del alcance como los valores de Key y Mode, ya que contenían muchos valores nulos y no eran de importancia para las decisiones a tomar y de igual manera eliminar valores discrepantes, como números o diferentes símbolos en mis datos.
Lo siguiente que se hizo ya para el final fue unir las data set en una sola y así poder tener un mejor manejo de toda la información.

# Power BI

1- Hice una tabla que me sumara la cantidad de streams por cancion, para tener un dato más detallado.

2- Luego hice un conteo de la cantidad de canciones que se lanzaron por año, en el cual obtuve que en el   2023 se lanzaron 176 canciones y en el 2022 413 siendo este el mas alto.

3- Realice una tabla y un gráfico para saber cuántas canciones habían sido feat y cuantas un solo y así sacar mis conclusiones de que es lo mejor para el nuevo artista.

# Medidas de tendencia central y de dispersión
 Saque el promedio, max, min, desv.estandar… para cada una de estas variables, Apple, Spotify, Streams, Deezer, Shazam, tanto en playlists como en charts.
 Realice un line chart tanto de los streams a lo largo de los años como de la cantidad de canciones a lo largo de estos.

 ### Histogramas 

Para los histogramas use la siguiente fórmula 

```python
import pandas as pd
import matplotlib.pyplot as plt

# Los datos importados a Power BI se almacenan en un DataFrame llamado 'dataset'
df = pd.DataFrame(dataset)

# Crear el histograma
#solo cambie el dato de bpm y agrege el de las otras variables para obtener el de cada una y asi obtener mis resultados.
plt.figure(figsize=(10,6))
plt.hist(df['bpm'], bins=20, color='skyblue', edgecolor='black')

# Configurar el título y etiquetas
plt.title('Histograma de bpm')
plt.xlabel('Valores')
plt.ylabel('Frecuencia')

# Mostrar el gráfico
plt.show()

```
### Segmentación de cada variable

Lo realice con los resultados de mis cuartiles para saber el promedio de streams por categoría ya sea baja o alta. Use tablas Matrix.

# Conclusiones
### Conclusión 1

Para el nuevo artista, es esencial mantener un flujo constante de lanzamientos para mantenerse relevante y visible en las plataformas de streaming. Además, explorar diferentes estilos y colaboraciones puede atraer a una audiencia más amplia, y enfocarse en construir una base de seguidores leales a través de interacciones genuinas en redes sociales. Dado que las redes sociales son vitales y ampliamente utilizadas, una estrategia de marketing efectiva en estas plataformas puede impulsar al artista hacia el éxito.

1. Con este dato observamos que hay una relación positiva clara entre el número de playlists y los streams. Al validar que la presencia en múltiples playlists está estrechamente relacionada con un mayor número de streams, destacamos la importancia de implementar estrategias de marketing dirigidas a maximizar la inclusión en playlists para ayudar al nuevo artista a establecerse más rápidamente en la industria musical competitiva.
2. Y por último, vemos que más del 50% de las canciones son un featuring. Por ende, destacamos la importancia de buscar colaboraciones estratégicas. Trabajar con DJs y productores para crear versiones remix que puedan ser añadidas a playlists de diferentes géneros, o publicar videos en YouTube, reels en Instagram o TikTok que muestren el proceso creativo y la química entre los artistas, puede aumentar la visibilidad y los streams del nuevo artista.

### Conclusión

Basándonos en nuestros hallazgos, recomendamos que el nuevo artista se enfoque en colaborar con otros artistas para aumentar su visibilidad y buscar ser incluido en tantas playlists como sea posible. Además, es esencial lanzar música de manera constante para mantener la relevancia. Estas estrategias, combinadas con un análisis continuo y ajuste de tácticas, ayudarán al nuevo artista a establecerse más rápidamente y asegurar el éxito en la industria musical

Para maximizar la visibilidad, es importante asegurarse de que las canciones y playlists tengan títulos, descripciones y etiquetas optimizadas para aparecer en búsquedas relevantes dentro de la plataforma, utilizando palabras populares en el momento. También es recomendable tener un estilo acorde a las tendencias actuales e ir evolucionando con ellas.

### Adiciones Sugeridas

- **Análisis de métricas**: Utilizar herramientas de análisis de datos de Spotify para monitorear el rendimiento de las canciones y ajustar estrategias en tiempo real.
- **Engagement en redes sociales**: Organizar eventos en vivo, sesiones de preguntas y respuestas, y sorteos para aumentar la interacción con los fans.
- **Contenido multimedia**: Crear contenido de alta calidad, como videoclips, behind the scenes y entrevistas, para aumentar la conexión emocional con la audiencia.
- **Optimización de SEO musical**: Investigar y aplicar técnicas de optimización de motores de búsqueda específicas para música, para mejorar la visibilidad en plataformas de streaming y redes sociales.
