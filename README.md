![HenryLogo](https://d31uz8lwfmyn8g.cloudfront.net/Assets/logo-henry-white-lg.png)

# Datathon: 

 Tomando los dataset provistos, a continuacion va detalle:

 ## Que modelo elegi para el proble planteado: REGRESION LOGISTICA
 
 Por que Regresion Logistica, debido a la naturaleza del problema que como salida tendremos una variable binaria en el afan de identificar, nuestra futura efectividad en las entregas y logra identificar cuales puede ser  los causantes de los yerros, para asi trabajar en los mismos.

 Inmediatamente luego de la importacion de las bibliotecas necesarias y herramientas, iniciamos el EDA.
 -Lectura y carga del dataframe, en mi caso elegi llegar los archicos a formato CSV, para su posterior tratamiento.
 -Inicio con la busqueda de valores nulos, y me encuentro con un set completo, detalle no menor ya que ese punto lleva mucho analisis.
 -Luego de comprobar que no tiene valores faltantes, paso a investigar la variable de salida, contabilizando los valores de ambas posibilidades, nos encontramos con una diferncia positiva hacia el lado de las entregas que llegaron de modo efectivo, pero el desbalance no es exagerado.
 regresaremos mas adelante sobre ese punto.
 
 -Realizo una obervacion sobre la media de los precios para ver que resultados arroja, y no se encuentran precios exorbitantes o alejados de la media, se avanza, no se perfila como un elemento de peso en la incidencia, de momento no se quita nada y avanzamos.
 
 -Como tenemos features con caracteristicas de tipo string, las mismas deben ser trabajadas para que el modelo elegido para la tarea pueda hacer uso de esta informacion.
 -En este punto elegimos realizar el cambio de los elementos de dichas columnas con la generacion de "Variables Dummies"

 ##CREANDO LAS VARIABLES DUMMIES

 Para esto tomamos las columnas que necesitamos pasar a expresiones numericas, y generamos una lista con las mismas, para que con el metodo que nos provee Pandas, Get_Dummies, se generara una nueva columna por cada valor difente que posean estas columnas, en el mismo procedimiento, unimos las mismas al dataframe original, con esta accion crecera el numero de columnas del mismo.

 -Despejamos la columnas no numericas, pero ahora necesitamos saber de todo estas columnas cuales son las que mas impacto tienen en la variable de salida que es el tema de estudio.

 -Buscaremos mejorar el BALANCE del dataset por medio de la tecnica de Over-sampling, lo que se haces en esta instancia es obtener distinas muestras del dataset para homogeneizar los datos de salida con la intencion de balancear para tener un modelo sin tenencia hacia un lado o el otro de modo previo al entrenamiento. Al aplicar Over samplig, o sobre muestreo podemos observar como luego de realizado el procedimiento tendremos salidas para las 2 posibles varaciones de nuestra variable de salida de modo balanceado, lo que nos indica que estamos en condiciones de trabajar ya obvservando las mejores FEATURES,  para quedarnoslas y aplicarles el model de ML.

 -Una vez hecho este procedimiento se obtiene un balance entre los resultados en la varible de salida. notorio en la grafica.

 -Luego de esto queremos depuarar estas columnas e ir a fondo con cuales son las que afectan el comportamiento de la salida.
 -Para esto buscaremos determinar cuales de estos features son importantes para el trabajo con nuestro modelo de Regresion Logistica, nos valdremos del metodo RFE que nos genera un ranking de las features que mas inciden en el resultado para poder utilizarlar y asi descartar columnas que no aportan valor core del analisi, entre las caracteristicas de esa manera podremos acercarnos a un mejor resultado.

 -Una vez determinadas las columnas que nos aportan al modelo, nos diponemos a colocarlas en una lista para poder filtrar estas columnas y quedarnos con los regresores que son lo que si debemos usar en nuestro modelo, desde luego que nos quedaremos con las que nos muestra la herramienta como regresores TRUE.

 -Para continuar generamos la lista con las columnas que si trabajaremos, nos valemos de esto de la libreria itertools y del metodo compress, que nos ayuda a limpiar esta ultimo paso del EDA ya de cara a implementacion.

 -Hecho esto nos disponemos a organizar nuestra informacion, ya de cara al armado del split y modelado, asignamos a  nuestras variables con las columnas que surgieron del trabajo previo para quedarnos con las que resultaron positivas en el ranking hecho con RFE, y quedamos de cara a la implementacion del modelo donde obtenemos un valor de 0.70.

 
## Logística del comercio mundial

La logística es un mercado vital en el mundo globalizado y conectado donde vivimos, coordinar el transporte de toda la cadena de suministros desde donde son producidos los bienes hasta que llegan al cliente final es una tarea compleja, que debe ser planificada y ejecutada correctamente para el funcionamiento del comercio, tanto local como mundial. 

Gracias a las nuevas herramientas como el uso de geolocalizadores, registros digitales de entrada/salida de los centros de distribución, distintos medios de transporte terrestres, marítimos y aéreos, además de las herramientas de IoT en toda la cadena de suministro y producción, es posible acumular muchísimos datos, que pueden ser analizados para optimizar los procesos logísticos.

## Descripción del problema

Somos parte de una empresa de logística que trabaja para un portal importante de E-Commerce, y nuestro Team Leader nos da la tarea de implementar un modelo que nos permita predecir si un envío llegará a tiempo o no, según la información contenida en el dataset puesto a disposición para poder prestar atención y mejor seguimiento a aquellos envíos que pueden llegar a dar problemas.

 
## Métrica a utilizar

Como método de evaluación del desempeño del modelo, se utilizará Exhaustividad (Recall) de la matriz de confusión (Confusion Matrix)

$$ Recall=\frac{TP}{TP+FN}$$

siendo $TP$ los verdaderos positivos, $TN$ verdaderos negativos y $FN$ los falsos negativos.

## Archivos provistos

Se proveen los archivos:
- 'E-Commerce_train.xlsx', con 8998 observaciones y 12 dimensiones, incluyendo información sobre si el envío llegó a tiempo o no en el momento del registro. 
- 'E-Commerce_test.xlsx', con 2000 observaciones y 11 dimensiones, sin incluir información sobre si el envío llegó a tiempo o no en el momento del registro.

## Descripción de las dimensiones

- ID: identificador del registro de orden (valor entero).
- Warehouse_block: Almacén de distribución de donde salió la orden (A a F).
- Mode_of_Shipment: Medio de transporte (Flight, Road, Ship).
- Customer_care_calls: Número de llamadas a atención al cliente que hubo por esa orden. (valores enteros del 2 al 7)
- Customer_rating: Puntaje del cliente (valores enteros 1 al 5).
- Cost_of_the_Product: Costo del producto (valor numérico entero de 96 a 310).
- Prior_purchases: Número de compras previas realizadas por el cliente (valor numérico entero de 2 a 10).
- Product_importance: Nivel de importancia del producto (low, medium, high).
- Gender: Género del comprador (F, M).
- Discount_offered: Porcentaje de descuento ofrecido por esa compra (valor numérico entero de 1 a 65):
- Weight_in_gms: Peso del paquete de la orden, en gramos (valor numérico entero de 1001 a 7846).
- Reached.on.Time_Y.N: Información sobre la llegada del paquete a destino (1 si llegó a tiempo, 0 si no llegó a tiempo).


 