- [Estadistica Descriptiva](#estadistica-descriptiva)
  * [Muestra](#muestra)
  * [Variable Aleatoria](#variable-aleatoria)
    + [VA Discreta](#va-discreta)
    + [VA Continua](#va-continua)
  * [Frecuencia](#frecuencia)
  * [Medidas de Centralizacion](#medidas-de-centralizacion)
    + [Media](#media)
    + [Mediana](#mediana)
    + [Moda](#moda)
  * [Medidas de Dispercion](#medidas-de-dispercion)
- [Estadistica Inferencial](#estadistica-inferencial)
  * [Muestreo](#muestreo)
    + [Muestreo Aleatorio](#muestreo-aleatorio)
      - [Muestra Aleatoria con reposicion](#muestra-aleatoria-con-reposicion)
      - [Muestra Aleatoria sin reposicion](#muestra-aleatoria-sin-reposicion)
    + [Muestreo Sistematico](#muestreo-sistematico)
    + [Muestreo Estratificado](#muestreo-estratificado)
    + [Muestreo por conglomerados](#muestreo-por-conglomerados)
    + [Muestreo polietapico](#muestreo-polietapico)
- [Estadistica Multivariante](#estadistica-multivariante)
- [Probabilidad Basica](#probabilidad-basica)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# Estadistica Descriptiva

## Muestra
Subconjunto de algo mas grande, de una población<br />
- Necesitamos una muestra aleatoria simple 
- La muestra tiene que ser representativa de la poblacion

## Variable Aleatoria
Lo que vamos a medir, por ejemplo, de una poblacion de personas podemos medir la altura, sexo, peso, etc..<br />
Existen 2 tipos de VA:

### VA Discreta
Que se puede contar, ejemplo: sexo, ciudad, etx..

### VA Continua
Valores reales que dificilmente sean repetidos, ejemplo: peso, altura, etc..


## Frecuencia

- **Frecuencia Absoluta:** Cantidad de veces que se repite
- **FA Acumulada:** Acumulacion de freccuencia absoluta
- **Frecuencia Relativa:** Que porcentaje del total representa
- **FR Acumulada:** Acumulo frecuencia relativa
<br />

| clase             | Frecuencia Absoluta | FA Acumulada | Frecuencia Relativa | FR Acumulada |
|-------------------|---------------------|--------------|---------------------|--------------|
| Muy Satisfactorio | 10                  | 10           | 10/25               | 10/25        |
| Satisfecho        | 7                   | 17           | 7/25                | 17/25        |
| Medio Satisfecho  | 5                   | 22           | 5/25                | 22/25        |
| Descontento       | 3                   | 25           | 3/25                | 25/25 = 1    |
|                   | Total = 25          |              | Total = 1           |              |

## Medidas de Centralizacion

### Media
Es el promedio<br />
<img src="https://latex.codecogs.com/svg.image?\bar{x}&space;=&space;\frac{\sum_{i&space;=&space;1}^{7}&space;x_{i}}{7}" title="\bar{x} = \frac{\sum_{i = 1}^{7} x_{i}}{7}" />

### Mediana
Ordeno valores de menor a mayor y elijo el que esta en el medio, si hay valores pares se hace promedio de los 2 valores que quedan

### Moda
Valor que mas se repite

## Medidas de Dispercion

# Estadistica Inferencial 
Mediante una muestra quiero poder llegar a describir lo mas certeramente posible la poblacion total.<br /><br />
Pasos para un estudio Inferencial:
- Establecer la caracteristica que se desea estimar o la hipotesis que se desea constatar
- Determinar que informacion nos hace falta para hacerlo
- Se diseña un experimento que permita recoger estos datos, este paso incluye
  * Decidir que tipo de muestra se va a tomar y su tamaño
  * Elegir las tecnicas adecuadas para realizar las inferencias deseadas a partir de la muestra que se tomara
- Tomamos esa muestra y medimos los datos deseados sobre los individuos que la forman
- Aplicar las tecnicas de inferencia elegidascon el software adecuado (Python o R)
- Obtener conclusiones
- Si las conclusiones son fiables y suficientes, redactar un informe; en caso contrario, volver a empezar.
<br />
<img src="images/7.png" />

## Muestreo
Tendremos que distinguir entre **Poblacion** y **muestra** (subconjunto de la poblacion)<br />
Dos tipos de analisis estadisticos:
- **Exploratorio** o **Descriptivo**: **Estadistica Descriptiva**
  * desribimos lo que viene de la muestra
- **Inferencial** o **confirmatorio**: **Estadistica Inferencial**
  * mediante una muestra quiero poder llegar a describir la poblacion
<br /><br />

### Muestreo Aleatorio
Consiste en seleccionar una muestra de la poblacion de manera que todas las muestras del mismo tamaño sean equiprobables (El tipico caso de las bolas)<br />

#### Muestra Aleatoria con reposicion
<img src="images/1.png" /><br />
Las bolas pueden salir mas de una vez

```r
sample(1:100, 15, replace=TRUE) # Elegimos 15 al azar
```

```r
head(iris)

set.seed(4) # seteamos una semilla para que los valores aleatorios sean siempre iguales

flores.elegidas = sample(1:150,10, replace= TRUE) #Elegimos 10
muestra.iris = iris[flores.elegidas,]
```

#### Muestra Aleatoria sin reposicion
<img src="images/2.png" /><br />
No puede salir una bola 2 veces

```r
sample(1:100, 15, replace=FALSE) # Elegimos 15 al azar sin repetir
```
Se puede considerar que con reposicion y sin reposicion son equivalentes si el tamaño de la poblacion es muy grande en relacion a la muestra (al menos una 1000 veces mayor)

### Muestreo Sistematico
Suponiendo que los individuos de una poblacion vienen de una lista ordenada, se toman en intervalos constantes escogiendo al azar el primer individuo<br />
En este caso elegimos uno al azar (el 92) y vamos contando de intervalos (en este caso 7)<br />
<img src="images/3.png" /><br />

```r
primer.valor = sample(1:150,1) # Elegir el primer valor
incremento = floor(150/10) # de las 150 quiero elegir 10

# long total de 10 elementos
# pero de esta manera puede pasa los 150
# si eligo como primera 130 van: 130, 140, 150, 160, 170,...
elegidas = seq(from=primer.valor, by=incremento, length.out=10) 

# para esto lo que hacemos es aplicar el modulo que me devuelve el resto
# si es 160 me daria 10
elegidas = elegidas%%150

muestra = iris[elegidas,]

```

### Muestreo Estratificado
Selecciono entre estratos, por ejemplo entre hombres y mujeres<br />
<img src="images/4.png" /><br />
La idea seria tomar una muestra aleatoria proporcional a cada una, en este ejemplo tomariamos 6 del primer color y 9 del segundo, siendo un total de 15


### Muestreo por conglomerados
Cuando el proceso de obtener y estudiar una muestra aleatoria es dificil<br />
En este caso en lugar de extraer muestras aleatorias, escogemos primero un subconjunto al azar. Esto lo llamamos por **cluster**<br />
Ej: en lugar de ir a diferentes personas podriamos ir a un edificio y encuestarlos ahi, seria menos costoso<br />
<img src="images/5.png" /><br />
En este ejemplo supongamos que son 20 edificios con 5 personas cada uno y elegimos 3 conglomerados<br />

```r
#Suponiendo que quiero medir jugadores de un mundial, y en este caso eligo 4 paises

numero.paises.elegidos = sample(1:32,4,replace=FALSE) # De 32 paises elijo 4
paises.elegidos = unique(wolrdcup$Team)[numero.paises.elegidos] # me traigo los paises

# me traigo los jugadores de esos 4 paises
muestra.worldcup = worldcup[wolrdcup$Team%in%paises.elegidos]
```

### Muestreo polietapico
Igual que por conglomerado pero selecciono aleatoriamente dentro de cada grupo<br />
<img src="images/6.png" /><br />

```r
#Suponiendo que quiero medir jugadores de un mundial, y en este caso eligo 4 paises

numero.paises.elegidos = sample(1:32,4,replace=FALSE) # De 32 paises elijo 4
paises.elegidos = unique(wolrdcup$Team)[numero.paises.elegidos] # me traigo los paises

# Me traigo los jugadores de cada pais (de los 4)
worldcup.pais1 = worldcup[wolrdcup$Team == paises.elegidos[1],]
worldcup.pais2 = worldcup[wolrdcup$Team == paises.elegidos[2],]
worldcup.pais3 = worldcup[wolrdcup$Team == paises.elegidos[3],]
worldcup.pais4 = worldcup[wolrdcup$Team == paises.elegidos[4],]

# Elijo 5 jugadores de cada pais
jugadores.pais1 = sample(1:dim(worldcup.pais1)[1],5,replace=FALSE)
jugadores.pais2 = sample(1:dim(worldcup.pais2)[1],5,replace=FALSE)
jugadores.pais3 = sample(1:dim(worldcup.pais3)[1],5,replace=FALSE)
jugadores.pais4 = sample(1:dim(worldcup.pais4)[1],5,replace=FALSE)

# Juntamos la muestra
muestra.worldcup = rbind(
  worldcup.pais1[jugadores.pais1,],
  worldcup.pais2[jugadores.pais2,],
  worldcup.pais3[jugadores.pais3,],
  worldcup.pais4[jugadores.pais4,]
  )
```

# Estadistica Multivariante

# Probabilidad Basica
