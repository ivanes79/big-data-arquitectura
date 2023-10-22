
# Diseño del DAaaS

## Definición la estrategia del DAaaS

- Página Web para consultar el catálogo de setas. En este catálogo, el cliente puede acceder a toda la información  a cada tipo de seta como morfología, valor culinario,    lugar en los que se encuentra,etc
- El cliente puede consultar una predicción de la posibilidad de encontrar setas por provincia, analizando los datos climáticos consultados en la base de datos teniendo en cuenta el ciclo de eclosión de las setas y sus características 


## Arquitectura DAaaS


- Fuentes de datos:
  - Crawler de <https://www.fungipedia.org>
  - Api aemet
- Componentes:
  - Google cloud storage para almacenar la información de cada seta e imagenes y    para almacenar los datos que obtenemos del api aemet
  - Cloud function con un schedule para consultar diariamente los datos climáticos  y almacenarlos en el bucket
  - postgreSQL donde almacenamos los datos de las setas en un tabla obtenidas en el crawler  y en otra tabla almacenamos los datos climáticos obtenidos. En ambos casos los datos los obtenemos de google storage en donde los hemos guardado y dado el formato correspondiente. Si la utilización de la tabla de clima aumentara , se estudiaría la posibilidad de hacer una base de datos externa con un postgre o un hadoop aparte para el buen funcionamiento de la base de datos
  - Pagina Web




## DAaaS Operating Model Design and Rollout

- Lanzar crawler (google function: manualmente) sobre pagina web <https://www.fungipedia.org> , obtener los datos y almacenar en el bucket de google cloud
- Crear cloud function y schedule para consultar diariamente api de aemet .Estos datos se almacenan en el bucket de google cloud para después acceder a ellos por provincia y hacer una predicción de la posibilidad de eclosión de setas
- Crear postgresql para crear las tablas :
- Tabla de setas: en ella se almacena los nombres de cada tipo de seta y toda información de cada una para que el usuario acceda a ella de forma rápida
- Tabla climatológica : en ella se guardan diariamente todos los datos climatológicos necesarios para que el predictor haga las operaciones necesarias que nos de la probabilidad de encontrar setas en esa fecha en cada provincia
- Crear una página web con el web server. El usuario entra en la página y accede a un catálogo de setas, pulsando en cada una de ellas para ver fotos  y sus características. La página web accede a las tablas de las setas y a la tabla de climatología para dar al usuario la probabilidad de encontrar setas , seleccionando la provincia en la que quiere la predicción
 






## Link a Diagrama

[Esquema]https://github.com/ivanes79/big-data-arquitectura/blob/main/Websetas.drawio.png
