Resuelve problemas que requieren de procedimientos estadísticos descriptivos, de acuerdo a requerimientos.
- IL1 Define población, muestra y tipos de variables presentes en un estudio, de acuerdo al contexto y a la naturaleza de los datos dados.
	- Poblacion: Todo el conjunto al cual engloba nuestros datos
	- Muestra: Seleccion especifica la poblacion la cual es medible y manejable
	- Tipos de Variable: 
		- Cuantitativas(Numero)
			- Continua(Numeros Decimales)
				- Ejemplo: El peso o la altura
			- Discreta(Numeros Enteros)
				- Ejemplo: El numero de hijos
		- Cualitativas(Cualidades)
			- Ordinal(Sigue un orden Natural o Jerarquico)
				- Ejemplo: Nivel Socieconomico o nivel educacional
			- Nominal(No Sigue ningun orden)
				- EJemplo: Genero o Color de pelo

- IL2 Interpreta los elementos de una tabla de frecuencia, de acuerdo a un contexto específico.
	- Elementos de tabla frecuencia:
		- Frecuencia Absoluta -> f -> numero
		- Frecuencia Relativa -> h -> porcentaje
		- Frecuencia Aboluta Acumulada -> F -> numero sumado ↓
		- Frecuencia Relativa Acumulada -> H -> porcentaje sumado ↓


Ejemplos del Examen
1.- Cual es la muestra obtenida por este estudio
550 clientes de telefonia movil de Santiago, año 2019

2.- Cual es la poblacion a la que hace
Todos los clientes de telefonia movil de Santiago, año 2019

3.- Identifique las Variables y Clasifiquelas
Pago_Mensual($): Cuantitativa Continua
Genero: Cualitativa Nominal
Compañia: Cualitativa Nominal
Permanencia en la compañia: Cuantitativa Discreta
Impuesto Adicional($): Cuantitativa Continua

4.- Complete la tabla adjunta con la informacion de la tabla de frecuencias en la hoja de desarrollo:
4.1- f4 -> 117 -> 117 Clientes tienen una permanencia en la empresa entre 4,5 y 6 años
4.2- h6 -> 4,4% -> 4,4% de los clientes tienen una permanencia en la empresa entre 7,5 y 9 años
4.3- F3 -> 237 -> 237 clientes tienen una permanencia en la empresa entre 0 y 4.5 años
4.4- H5 -> 95,6 -> 95.6% de los clientes tienen una permanencia en la empresa entre 0 y 7,5 años

- IL3 Interpreta un gráfico de acuerdo a un contexto específico, considerando sus aspectos más relevantes.
5.- Construya un grafico apropiado para la variable COMPAÑIA. comente los aspectos mas relevantes
5.1- La mayoria de los clientes prefirieron la compañia ENTEL
5.2- La mayoria de los clientes prefirieron la compañia Movistar
5.E- Se eligio un grafico de torta e histograma, ademas de la tabla dinamica porque es Cualitativa nominal
5.ED- Valores -> Generos, Generos2 / Columnas -> Valores / Filas -> Compañia
5.EH- Se copiaron los valores de la tabla dinamica a mano para hacer un grafico con la cuenta de generos, para ver su distribucion por compañia (Activando Etiqueta de datos), cambiando el nombre el titulo del eje en ambos lados del grafico
5.ET- Que se vea igual que el otro grafico, y que la leyenda salga a un lado para que se vea bonito


- IL4 Calcula la media, moda y mediana a partir de una base de datos, usando herramientas de Excel.
6.- Calcula las medidas de tendencia central para la variable PAGO_MENSUAL e interpretalas
- Media: 
	- Se calcula: `=PROMEDIO(HOJA_BASE_DATOS!INICO:FINAL)`
	- Se interpreta: El promedio que realizan la "Muestra" es de "Monto_Calculo"
- Moda: 
	- Se calcula: `=MODA(HOJA_BASE_DATOS!INICO:FINAL)`
	- Se interpreta: El "Accion" mas frecuente que realizan los "Muestra" es de "Monto_Calculo"
- Mediana: 
	- Se calcula: `=MEDIANA(HOJA_BASE_DATOS!INICO:FINAL)`
	- Se interpreta: El 50% de los pagos que han realizado los "Muestra" es menor o igual a "Monto_Calculo"
- Bases de datos: 
	- Formulas Excel: 

8.- Cuanto pagaria como maximo un cliente que esta entre el 35% de los clientes que menos pagan
- IL5 Calcula percentiles de variables a partir de una base de datos, usando herramientas de Excel.
	- Percentil: 
		- Se calcula: `PERCENTIL(HOJA_BASE_DATOS!INICIO:FINAL;PERCENTIL%)`
		- Se interpreta: Un "Muestra" que es en el "Percentil%" de los que menos pagan, tendria una tarifa de como maximo "Monto_Calculado"

7.- Realice Observaciones importantes, Existen graficos Simetricos (Se reparten igual entre ambos extremos) Asimetrico (No lleva orden), Ascendente (Los valores solo suben) y descente (Los valores solo bajan)
- La mayoria entre "DATOS MAX", La minoria entre "DATOS MIN", Todos ENTRE "MAX y MIN"


9.- Las empresas de telecomunicaciones desean crear un impuesto para el 16% de las llamadas con mayor pago mensual ¿cual es le rango de tarifas que serian gravadas con este impuesto?
- 100-16=84 -> =PERCENTIL(Hoja_Base_Datos!INICIO:FINAL;84%)
	- El rango de tarifas que seran gravadas con el impuesto son todas aquellas mayores o iguales a "Monto_Calculado"

10.- Entre las empresas WOM y ENTEL, ¿Cual tiene un pago mensual mas disperso?
- Promedio y Desvest (Desviacion Estandar)
	- =DESVEST.P(INICIO:FINAL) Primero se debe hacer una 
	- =PROMEDIO(INICIO:FINAL)
	- Dividir DESVEST_Com1/Promedio_Com1 y DESVEST_Com2/Promedio_Com2
	- LA que salga con mayor % es la que tenga datos mas dispersos



Realice un grafico de dispersion para las variables PAGO_MENSUAL e IMPUESTO_ADICIONAL, el grafico debe contener el modelo de regresion Lineal, Exponencial y logaritmica, asi tambien el coeficiente de determinacion de cada uno de ellos. ¿Que modelo se adapta mejor a los datos, o es mas confiable?
- IL6 Compara la dispersión de dos o más grupos de datos utilizando medidas de dispersión.
	- Dispersion: El que tenga el coeficiente de determinacion mas alto es el que es mas confiable
		- Modelos: Regresion lineal, Exponencial y Logaritmica 
		- Formulas Excel: 

Resuelve problemas de fenómenos modelados por dos o más variables, utilizando modelos matemáticos y estadísticos descriptivos, de acuerdo a requerimientos.
- IL7 Aplica el modelo de regresión lineal o exponencial para predecir valores de la variable dependiente.
	- Regresiones
		- Lineal: 
			- Excel: 
		- Exponencial: 
			- Excel:
- IL8 Construye un grafico de dispersión a partir de una base de datos, usando herramientas de Excel.
	- Grafico de Dispersion: 
		- Excel: 


Resuelve problemas de eventos probabilísticos relacionados con variables aleatorias, de acuerdo a requerimientos.
- IL9 Calcula la probabilidad de un evento aleatorio aplicando funciones de Excel.
11.- Contruya una tabla bidimencional de distribucion de frecuencias relativas utilizando las variables Genero y Compañia
11.-a Si se elige al azar a un cliente, ¿Cual es la probabilidad de que tenga por compañia movistar y sea hombre? Ver la probabilidad que genera la Tabla dinamica de los datos Compañia (Filas) y Genero (Columnas)
11.-b Si se elige al azar a un cliente, ¿Cual es la probabilidad de que tenga por compañia Entel y Movistar?


Extras:

mínimo -> `=min(Y;Y)`
máximo -> `=max(Y;Y)`
Tabla de frecuencias variables cuantitativas continuas
n° Intervalos(Regla de Sturges) -> `=redondear(1+3,3*log10(Vtotal);0)`
rango -> `=Vmax-Vmin`
amplitud -> `redondear.mas(Vrango/N°inter;n°Decimales)`

