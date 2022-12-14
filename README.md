# Trabajo 02 Riesgo de Credito
 
## Introduccion
Para este trabajo crearemos una aplicacion que permita a un usuario en base , a su informacion financiera le permita predecir como sera su scorecard , ademas mostrará si es mayor o menor que la población.
 
Para esto tomamos un dataset que esta disponible en kaggle , este contiene información corceniente a datos de los prestamos de clientes recopilados por la compañia Lending Club, una compañia de prestamo P2P (Peer-to-Peer), la informacion contiene alrededor de 450000 registros de prestamos de clientes entre el año 2007 a 2014, con alrededor de 75 variables que nos indican informacion sobre los clientes y el prestamo.
 
## Eliminacion de variables
 
Primero para garantizar mas exactitud en el modelo , eliminamos variables que cuenten con un gran porcentaje de nulos, precisamente , eliminamos variables que posean 80% de datos nulos.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/01.PNG)
 
Lo siguiente sera eliminar variables con informacion que no es relevante para el modelo.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/02.PNG)
 
## Identificacion de la variable objetivo
 
Primero encontramos la variable que nos interesa predecir , la cual es loan status , primero visualizamos como esta distribuidan sus diferentes valores unicos, una vez visualizados , necesitamos transformar la variable de forma que nos interese predecir, primero separamos los valores de loan status que tienden a mostrar que una persona es una buena o mala opcion para darle un prestamo, y luego eliminamos la columna de loan status original
 
Las variables que deciden si una persona no es buena opcion para un prestamo son (Charged Off', 'Default', 'Late (31-120 days)','Does not meet the credit policy. Status:Charged Off'), a estas personas se les asignara un 0 , y al resto de la poblacion se le asignara un 1. Convirtiendo asi la variable objetivo en un 0 siendo mala opcion y un 1 una buena opcion.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/03.PNG)
 
## Dividir el dataset
Dividimos el dataset en entrenamiento y validacion , con una relacion de 80 y 20 rspectivamente del dataset original.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/04.PNG)
 
## Manejo de datos
Ahora manejamos variables con informacion que en la manera que esta , no se puede digitar en un modelo, primero transformamos la variables emp_length ( el cual es años trabajando) , eliminamos toda cadena de texto , y en caso de ser especificamente trabajando menos de un año se vuelve 0 , ya despues de eso tenemos unicamente, datos numericos , en formato cadena , asi que transformamos en formato numerico los numeros.
 
Asi para otras variables que necesiten algun manejo de datos se aplicara una funcion que las modifique.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/05.PNG)
 
## Seleccion de variables
Usando el metodo de chi cuadrado encontramos posibles variables para el modelo
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/06.PNG)
 
Usando el analisis de varianza usando el estadistico F, encontramos las siguientes variables para el modelo.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/07.PNG)
 
## Mapa de coorelacion
 
Usando las 20 primeras variables, grraficamos el mapa de coorrelacion para poder obtener como se relacionan entre si.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/08.png)
 
siendo que out_prncp_inv y total_pymnt_inv tienen una alta coorelacion se eliminan.
 
## WOE
Luego de haber seleccionado las variables , y haberles aplicado metodo de one hot encoding para que sean aptas para el modelo, se comienza la parte de la ingenieria de caracteristicas
 
Para esto calculamos el WOE( peso de evidencia ) y el IV(Valor de informacion) estas tecnicas para ingenieria de caracteristicas son ampliamente usadas en puntajes crediticios.
 
el WOE usa la formula de logaritmo natural de la division entre el porcentaje de buenos clientes sobre malos clientes mientras que el IV es una sumatoria de el producto del WOE por la diferencia de porcentaje entre buenos y malos clientes, estas tecnicas las aplicamos a todas nuestras variables predictorias
 
En la siguiente imagen mostramos un ejemplo usando la variable revol_util
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/09.PNG)
 
## Modelo inicial
Una vez obtenido el modelo  , usando regresion logistica y usando validacion cruzada obtenemos un modelo de prediccion de si una persona es buen o no cliente
con esto vemos que tanto el puntaje GINI como AUROC , son bastante buenos por lo tanto se acepta el modelo.
 
![](https://github.com/Efbarrientosa/Trabajo-2-TAE/blob/main/10.PNG)
 
## Modelo del Scorecard
 
Por ultimo creamos un Scorecard, para esto usaremos los rangos sugeridos para los puntajes siendo de 300 a 850, con esto creamos coeficientes a partir de la suma de minimos y maximos de los valores obtenidos en cada variable , con los cuales obtendremos una calificacion para cada variable, y luego las aplicamos sobre todo el dataset, usando anteriormente , el WOE , calculamos los puntajes para un set de datos dados y con eso se construye el modelo para la scorecard , al aplicarlo sobre el dataset original nos encontramos que la media de la poblacion ronda el puntaje de 549.198462 , ya como se obtuvo el modelo para prediccion , este se usara para predecir en base a las variables obtenidas , el score de una persona.

## Conclusiones
Como pudimos observar , la creacion de un modelo crediticio es una tarea minuciosa , que requiere una buena ingenieria y manipulacion de variables , gracias a eso , una persona con conocimiento suficiente de su situacion financiera puede encontrar su propio scorecard y ver como se relaciona con la media o si es factible de que se le deba prestar o no un credito.

## Aplicacion 
[Link de la aplicacion](https://ancgarciamo-trabajo02-trabajo02tae-5uwqna.streamlit.app/) 

## Video promocional 

## Referencias 
[[1] How to Develop a Credit Risk Model and Scorecard](https://towardsdatascience.com/how-to-develop-a-credit-risk-model-and-scorecard-91335fc01f03)<br>
[[2] How to Develop a Credit Risk Model and Scorecard - github](https://github.com/finlytics-hub/credit_risk_model/blob/master/Credit_Risk_Model_and_Credit_Scorecard.ipynb)<br>
[[3] Streamlit](https://streamlit.io/)<br>
[[4] Stackoverflow](https://stackoverflow.com/) 
