# Análisis de precios históricos de commodities agrícolas 2005-2025

Este proyecto analiza la evolución histórica de precios y volatilidad de soja, maíz y trigo durante el período 2005-2025, utilizando como fuente los contratos de futuros del Chicago Board of Trade (CBOT) la referencia internacional de precios para estos granos y la base sobre la que se forman los precios en los principales mercados exportadores del mundo, incluyendo Argentina.

Vale aclarar que este es un análisis de precios internacionales de referencia. Adaptar estas series a la realidad local de un mercado como el argentino, requiere incorporar variables adicionales como retenciones, tipo de cambio y base, lo que excede el alcance de este proyecto.

## Metodología y Datos

El proyecto replica un flujo de trabajo habitual en el análisis de datos aplicado al agro: extracción automatizada de datos con Python, procesamiento y análisis exploratorio en Excel.

Los datos fueron descargados mediante un script en Python desde fuentes públicas de información financiera, construyendo un dataset diario desde 2005 hasta 2025 que puede actualizarse fácilmente. Una vez obtenidos, los datos fueron procesados en Excel, estandarizando fechas, organizando las series por commodity y seleccionando las variables relevantes para el análisis. 

## Analisis

El análisis se estructura en cinco ejes principales. En primer lugar se estudió la evolución histórica de precios para identificar tendencias y ciclos de largo plazo. A partir de los precios diarios se calculo su retorno, es decir, su variación porcentual del precio de un día al siguiente expresada en escala logarítmica, que son la base para los análisis siguientes.

Con esos retornos se midió la volatilidad histórica mediante una ventana móvil de 40 ruedas de trading, es decir, 40 días hábiles de mercado, aproximadamente dos meses, anualizada para facilitar su interpretación. Esta métrica permite identificar períodos de mayor incertidumbre en el mercado sin depender de un único valor estático.

Para facilitar la comparación entre los tres commodities, que cotizan en escalas de precio muy distintas, se construyeron series de precios normalizados, que ponen a los tres en una base común de 100 y permiten comparar su performance relativa a lo largo del tiempo.

Finalmente se analizó la correlación entre los retornos de los tres commodities, evaluando en qué medida tienden a moverse en la misma dirección.

#### Análisis de evolución de precios
Se analizó la evolución histórica de los precios de cierre de los tres commodities durante el período 2005-2025, mediante gráficos de series temporales. El análisis permite identificar tres ciclos alcistas diferenciados a lo largo del período. 

![](Graficos/closeanual.png)

El primero en 2007-2008, impulsado por la crisis alimentaria global. El segundo en 2010-2013, marcado por sequías severas en las principales zonas productoras. El tercero en 2021-2022, combinando la reactivación post pandemia y el shock de oferta generado por la guerra en Ucrania.

Entre estos ciclos el mercado atravesó períodos de estabilización con precios laterales, particularmente entre 2014 y 2020, donde los tres commodities fluctuaron en un rango acotado.

A nivel individual, la soja mostró los precios más elevados del período, operando consistentemente por encima de los otros dos commodities. El maíz y el trigo mostraron niveles de precio más similares entre sí.

#### Análisis de volatilidad
Se calculó la volatilidad histórica anualizada mediante una ventana móvil de 40 ruedas de trading, utilizando retornos logarítmicos diarios. Los valores se expresan en porcentaje anual.

En condiciones normales de mercado, los tres commodities operaron en un rango de volatilidad de entre 15% y 35%, con el trigo mostrando consistentemente niveles más elevados que el maíz y la soja.

![[Volatipidad entero.png]]

El período analizado presenta cuatro eventos de volatilidad extrema claramente identificables:

Crisis financiera global 2008: El evento más severo del período para soja y trigo, con la soja alcanzando casi 97% y el trigo superando el 70%. La crisis global impactó simultáneamente todos los mercados de commodities, generando una caída abrupta de precios seguida de alta incertidumbre.

Maíz 2013:  El maíz registró un pico aislado cercano al 75%, no replicado en soja ni trigo. Este comportamiento diferencial sugiere un factor específico del mercado de maíz en ese período.

Maíz y soja 2021: Ambos commodities superaron el 60%, impulsados por compras masivas de China y una sequía severa en Sudamérica que redujo la oferta global en un contexto de fuerte reactivación económica post pandemia.

Guerra en Ucrania 2022: El trigo alcanzó casi 90% de volatilidad anualizada entre marzo y mayo, el pico más alto del período para este commodity. Rusia y Ucrania representan aproximadamente el 30% de las exportaciones mundiales de trigo, y el conflicto generó un shock de oferta inmediato y severo.

La mediana de volatilidad osciló entre 20% y 30% según el commodity, mientras que los valores máximos superaron el 75% en los tres casos. En los tres commodities la media resultó mayor que la mediana, lo que indica que la distribución de volatilidad está sesgada hacia arriba con picos extremos asociados a eventos puntuales que elevaron el promedio, pero la mayor parte del tiempo el mercado operó por debajo de ese valor. Se puede decir que el mercado fue relativamente estable en el día a día, pero cuando se movió lo hizo con fuerza.

El trigo fue el commodity con mayor presencia en zona de estrés, superando el 40% de volatilidad anualizada el 17% del tiempo analizado. El maíz registró un 12% y la soja un 6%, confirmando que los picos de soja fueron eventos puntuales e intensos, como la crisis de 2008, mientras que el trigo mostró una inestabilidad más persistente a lo largo del período.

A partir de 2023 los tres commodities retomaron niveles de volatilidad dentro del rango histórico normal, sugiriendo una normalización gradual de los mercados agrícolas globales.

#### Comparación de desempeño mediante precios normalizados
Para facilitar la comparación entre commodities con distintos niveles de precio, se construyeron series de precios normalizados. Este procedimiento es necesario porque comparar precios absolutos entre commodities no tiene sentido ya que si la soja cotiza cerca de 1400, el maíz cerca de 600 y el trigo cerca de 750 graficar las tres series juntas distorsionaria la comparación.

La normalización se realizó mediante la siguiente fórmula:

Precio normalizado = (Precio_t / Precio_base) × 100

Donde el "Precio_base" es el precio de cierre del primer día disponible de cada commodity enero de 2005 y "Precio_t" es el precio de cierre de cada rueda. Esto fija un valor inicial común de 100 para los tres commodities, permitiendo observar la performance relativa a partir de ese punto. 
La normalizacion permite entender facilmente que si encontramos un valor de 150 indica que el precio subió un 50% respecto al inicio, mientras que un valor de 80 indica una caída del 20%.

#### Comparación de rendimiento acumulado
En este apartado se analizó la performance acumulada a lo largo del período 2005-2025.

Al cierre del período analizado, el maíz registró el mayor rendimiento acumulado con un valor normalizado de 218, equivalente a una suba del 118% respecto al valor inicial.
La soja finalizó en 191, acumulando un 91% de ganancia, mientras que el trigo fue el de menor performance con un valor final de 167, representando una suba del 67%.

![[Precios normalizados todo.png]]

Sin embargo, el análisis de máximos históricos revela una historia distinta. El trigo alcanzó el pico más alto de los tres commodities en 2022, llegando a 471, casi cinco veces su valor inicial, impulsado por el shock de oferta generado por la guerra en Ucrania. 
El maíz registró su máximo en 2012 con 412, en un contexto de sequía severa en Estados Unidos, uno de los mayores productores mundial, mientras que la soja también alcanzó su pico en 2012 con 329

|       | Rendimiento | Pico Maximo |
| ----- | ----------- | ----------- |
| Maiz  | 118%        | 412         |
| Soja  | 91%         | 329         |
| Trigo | 67%         | 471         |

Comparando esta informacion, se concluye con algo interesante, el trigo fue el commodity con el mayor pico histórico pero a la vez fue el que menor rendimiento acumulado tuvo al final del período, lo que sugiere que sus ganancias extremas no fueron sostenidas en el tiempo. El maíz, por otro lado, mostró una performance más consistente a largo plazo.

#### Resiliencia ante shocks
Este análisis busca responder dos preguntas concretas: qué tan fuerte golpeó cada crisis a estos mercados, y cuánto tardaron en recuperarse? Para responderlas se evaluaron tres condiciones en cada shock: qué tan profunda fue la caída, cuánto tiempo duró el período sin recuperación, y qué tan rápido volvió cada commodity a sus niveles previos.

Para medirlo se utilizó el drawdown histórico, una métrica que mide cuánto se ha alejado el precio de su máximo histórico más reciente. Un valor de 0 indica que el commodity se encuentra en su máximo. Los valores negativos muestran la magnitud de la caída respecto a ese punto, por ejemplo, -0.20 significa que el precio está un 20% por debajo de su máximo previo, mientras que -0.60 indica una caída del 60%. Cuanto más negativo es el valor, mayor es la distancia respecto al pico anterior. Cuando el drawdown vuelve a 0, significa que el precio ha recuperado completamente ese máximo o ha alcanzado uno nuevo.

![[dd anual.png]]

Durante el período 2005-2025 se presentan tres episodios de estrés claramente identificables:

Crisis financiera global 2008: El shock más abrupto del período. Los tres commodities cayeron simultáneamente, el trigo llegó a -0.60, el maíz a -0.50 y la soja a -0.45. A pesar de la profundidad de la caída, fue el shock con recuperación más rápida: para 2011 los tres habían vuelto a niveles cercanos a sus máximos. La soja fue el commodity más resiliente, combinando la caída menos profunda con la recuperación más veloz.

Caída sostenida 2013-2016: El episodio más prolongado del dataset. Después de los máximos de 2012 los tres commodities cayeron gradualmente y ninguno logró recuperar esos niveles durante casi siete años. El trigo alcanzó su "peor" momento histórico con un drawdown de casi - 0.70, es decir, llegó a valer un 70% menos que en su mejor momento. A diferencia del shock de 2008, esta caída no respondió a un evento puntual sino a una corrección estructural tras años de precios elevados. La duración es el rasgo más llamativo de este período.

Post guerra Ucrania 2022-2025: Tras los picos de 2022 los tres commodities iniciaron una nueva corrección que al cierre del período analizado aún no se ha revertido. El trigo y el maíz se encuentran entre - 0.50 y - 0.65, y la soja entre - 0.35 y - 0.40. Es el único shock del período donde todavía no hay señales claras de recuperación.

A lo largo de los tres episodios el trigo mostró consistentemente las caídas más profundas y las recuperaciones más lentas. La soja por el contrario demostró ser el commodity más resiliente en los tres casos. El maíz se ubicó en una posición intermedia en profundidad pero con períodos de recuperación prolongados, particularmente en el ciclo 2013-2020.

##### ¿Que commodity lidera el mercado?
En cada ciclo alcista uno de los commodities tiende a subir más que los otros, marcando el ritmo del mercado. Identificar qué commodity lidera en cada período es útil porque permite entender qué factor está dominando el mercado en ese momento, si es un shock de oferta global, un factor climático regional o un cambio en la demanda. El commodity que lidera es el que más expuesto esta al factor que está generando el movimiento.

Durante el ciclo 2007-2008 el trigo fue el líder indiscutido, alcanzando un valor normalizado de 420 mientras el maíz llegaba a 371 y la soja a 306. Esto refleja que la crisis alimentaria global de ese período impactó primero y con más fuerza al trigo, el cereal más consumido a nivel mundial.

En el ciclo 2010-2013 el liderazgo pasó al maíz, que alcanzó su máximo histórico del período con 412, superando a la soja en 329 y dejando al trigo rezagado. La sequía severa en el Corn Belt americano en 2012 fue el factor determinante del shock de oferta del maíz.

En el ciclo 2021-2022 el trigo recuperó el liderazgo con el pico más alto de todo el período, alcanzando 471 impulsado por el shock de oferta generado por la guerra en Ucrania.

Un patrón interesante a destacar es que a lo largo del período, la soja nunca lideró un ciclo alcista. Acompañó los movimientos del mercado pero sin ser el principal, lo que es coherente con su menor volatilidad mediana respecto a los otros dos commodities.

En conjunto, el análisis de precios normalizados muestra que los tres commodities comparten ciclos comunes impulsados por factores globales, pero con intensidades distintas según la naturaleza de cada shock. El trigo mostró los movimientos más extremos pero menor consistencia a largo plazo, mientras que el maíz demostró la mejor performance acumulada y la soja la mayor estabilidad relativa a lo largo del período.

#### Análisis de correlación entre commodities
La correlación permite evaluar en qué medida los precios de diferentes productos agrícolas tienden a moverse en la misma dirección. Este análisis es útil para comprender relaciones entre mercados agrícolas, posibles efectos comunes de factores globales y patrones de comportamiento compartidos entre commodities.

Para este análisis no se compararon los precios directamente sino las variaciones diarias (retornos logaritmicos) de cada commodity. Esto es necesario porque los tres precios tienen una tendencia general al alza a lo largo de 20 años y si se comparan los precios absolutos, la correlación aparece alta simplemente porque todos suben con el tiempo, no porque estén realmente relacionados. Usar las variaciones diarias elimina ese efecto y permite ver si los mercados realmente se mueven juntos o no.

La escala va de -1 a 1, donde valores cercanos a 1 indican que los commodities se mueven en la misma dirección, valores cercanos a 0 indican ausencia de relación y valores cercanos a -1 indican movimientos opuestos.

![](correlacion_commodities.png)


Los resultados de la tabla muestran correlaciones bajas y positivas entre los tres pares. El maiz contra la soja registró la correlación más alta con 0.28. Maiz contra trigo mostró 0.23, compartiendo factores climáticos y de demanda global. Soja vs trigo resultó la más baja con 0.15, la soja responde principalmente a la demanda de China mientras que el trigo es más sensible a factores geopolíticos como el conflicto en Rusia y Ucrania.

En conjunto, los mercados agrícolas comparten factores comunes como el clima global, los costos de energía y el valor del dólar, pero cada commodity responde a situaciones específicas.
La correlación baja entre los tres indica que diversificar entre estos activos tiene sentido desde una perspectiva de gestión de riesgo.


## Conclusion
El análisis de los precios históricos de soja, maíz y trigo durante el período 2005-2025 muestra que los mercados agrícolas combinan ciclos de crecimiento sostenido con episodios puntuales de alta volatilidad, generalmente asociados a factores climáticos, geopolíticos o shocks de demanda global.

Los tres commodities comparten una tendencia alcista de largo plazo, todos duplicaron su valor respecto al inicio del período, pero con dinámicas distintas. El trigo mostró los movimientos más extremos en ambas direcciones: los picos más altos y las caídas más profundas. La soja demostró ser el activo más estable, con menor volatilidad y mayor resiliencia ante shocks. El maíz ocupó una posición intermedia, con la mejor performance acumulada al final del período.

La correlación baja entre los tres confirma que, a pesar de compartir factores comunes como el clima global y el valor del dólar, cada commodity responde principalmente a sus propios drivers de oferta y demanda.

## Bibliografia

Yahoo Finance, fuente de los precios históricos de futuros agrícolas. finance.yahoo.com

Hull, J. (2010). _Options, Futures, and Other Derivatives_. Pearson Education.

Joachim, V. B., & Joachim, V. B. (2008). Food and financial crises: Implications for agriculture and the poor. En _AgEcon Search (University of Minnesota, USA)_ (Número 1). https://doi.org/10.22004/ag.econ.47663

_Cómo la invasión rusa de Ucrania ha agravado la crisis alimentaria mundial_. (2025). Consejo de la Union Europea. https://www.consilium.europa.eu/es/infographics/how-the-russian-invasion-of-ukraine-has-further-aggravated-the-global-food-crisis/

_Investopedia_. (s. f.). Investopedia. https://investopedia.com/

_Soja 20/21: la cosecha más baja de los últimos 10 años en la región_. (s. f.). Bolsa de Comercio de Rosario. https://www.bcr.com.ar/es/mercados/gea/seguimiento-de-cultivos/informe-semanal-zona-nucleo/soja-2021-la-cosecha-mas-baja-de

colaboradores de Wikipedia. (2024, 23 enero). _Crisis alimentaria mundial de 2007-2008_. Wikipedia, la Enciclopedia Libre. https://es.wikipedia.org/wiki/Crisis_alimentaria_mundial_de_2007-2008

##### Herramientas utilizadas
- Python — pandas, yfinance, matplotlib, seaborn
- Microsoft Excel — análisis exploratorio y visualización



