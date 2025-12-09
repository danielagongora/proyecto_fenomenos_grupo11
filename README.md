# proyecto_fenomenos_grupo11

## Descripción general del proyecto

El presente proyecto aborda la modelación del transporte de lixiviados a través de barreras semipermeables en un Relleno Sanitario.

Los derrames de lixiviados producidos por desechos que no son tratados óptimamente, provocan impactos graves en el medioambiente que tienen graves consecuencias sociales y económicas, y Chile no está exento de esta problemática.

Es por esto que surge la necesidad de fortalecer los suelos de los rellenos sanitarios donde se disponen finalmente los residuos sólidos con capas permeables que eviten el transporte de lixiviados.

En Chile, debido a los grandes problemas que provoca la deposición de lixiviados en los suelos, existen normas que regulan esta actividad, tales como la Ley 19300, que establece que todos los proyectos de saneamiento ambiental deben someterse al sistema de evaluación de impacto ambiental, y el Decreto Supremo N°46/2002, que tiene por objeto regular la descarga de contaminantes hacia aguas subterráneas, mediante la fijación de límites máximos permisibles para la descarga de residuos líquidos.

## Explicación breve sistema modelado

Para llevar a cabo la modelación del transporte, se consideró un sistema compuesto por tres capas: HDPE, arcilla compacta y tierra franco-arenosa. Para esto, se modeló un sistema cartesiano unidireccional con simetría del perfil de concentración en el plano horizontal, utilizando los siguientes supuestos:

**I.** Se excluyen del estudio los fenómenos de transferencia producidos en las paredes laterales del relleno sanitario.

**II.** El ancho de las capas del sistema es igual al mínimo establecido por la normativa chilena.

**III.** Debido al bajo espesor de la geomembrana, sus efectos se modelan como una condición de borde.

**IV.** El dominio del sistema empieza desde la superficie externa de la capa de arcilla compactada, que cuenta con un ancho mínimo de 60 cm y termina con una capa de tierra de 3 m.

**V.** Debido a la muy baja conductividad hidráulica del HDPE y la arcilla compactada, se considera que no existe transporte advectivo en estos materiales. En las capas inferiores, se asume que el término advectivo no es despreciable.

**VI.** Los contaminantes no reaccionan en el medio en que se transportan pero se incorpora término de decaimiento exponencial en el tiempo en la superficie externa de la geomembrana. Esto representa reacciones o descomposiciones que ocurren en el lixiviado acumulado antes de entrar en las capas del suelo.

**VII.** Propiedades físicas como el coeficiente de difusividad en un material son constantes en el espacio y en el tiempo. Se utilizarán valores reportados en la literatura asumiendo que son aplicables para el contexto del modelo.

**VIII.** Se desprecian los efectos de retención de solutos mediante adsorción y retención de agua. También se asume un sistema isotérmico y no se consideran efectos térmicos en la transferencia de materia. No se consideran fluctuaciones fluviales.

**IX.** Se desprecian las posibles interacciones entre contaminantes en el proceso de transferencia de masa, tales como competencia por sitios de sorción, reacciones y fenómenos de difusión cruzada.

La siguiente imagen representa el sistema modelado:

<p align="center">
  <img src="./imagenes/sistema.png" alt="Diagrama" width="400">
</p>

## Descripción del método numérico utilizado
Luego de realizar el balance de materia de un compuesto α en un volumen diferencial rectangular en una capa del sistema, se llegó a la siguiente ecuación gobernante:
<p align="center">
  <img src="./imagenes/ecuacion general.png" alt="Diagrama" width="200">
</p>
Además, debido a los supuestos considerados, se hace la distinción para las capas de arcilla y tierra. Por lo que para cada una se obtienen las siguientes ecuaciones gobernantes:

### Ecuación barrera de arcilla:

<p align="center">
  <img src="./imagenes/ecuacion arcilla.png" alt="Diagrama" width="200">
</p>

### Ecuación capa natural de tierra:

<p align="center">
  <img src="./imagenes/ecuacion tierra.png" alt="Diagrama" width="200">
</p>

De este modo,  las ecuaciones gobernantes para las capas corresponden a un balance de masa diferencial (transiente y 1-D) que considera transporte de los contaminantes sólo por difusión en la barrera de arcilla y además el arrastre advectivo en la capa de suelo.

En cuanto a las discretizaciones realizadas, se discretizó la ecuación gobernante de la barrera de arcilla para un contaminante dado (con su respectiva difusividad) mediante el método Forward Time-Centered Space (FTCS), lo cual se puede ver en la siguiente imagen:
<p align="center">
  <img src="./imagenes/discretizacion arcilla.png" alt="Diagrama" width="600">
</p>

Junto a esto, se discretizó la capa de tierra de la siguiente forma:
<p align="center">
  <img src="./imagenes/discretizacion tierra.png" alt="Diagrama" width="700">
</p>
