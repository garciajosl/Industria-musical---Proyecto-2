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

3- el siguiente es una tabla y un gráfico para saber cuántas canciones habían sido feat y cuantas un solo y así sacar mis conclusiones de que es lo mejor para el nuevo artista.

