# Plantilla de diseño — Encuesta de satisfacción (hito 1)

**Equipo:** Grupo 5

**Integrantes:** Ganchala Pavel, Lamiña Matias, Magarisca Bryan, Martínez Domenica, Medina Juan

**Fecha:** 20/10/2026

**Repositorio (fork):** https://github.com/pavexl/IDSD422-lab2-diseno-encuesta-grupo-5/blob/main/plantilla-encuesta.md

**Enfoque del equipo (aprobado en clase):** Variedad y stock: satisfacción y disponibilidad.

Completa cada sección. Usa commits por sección; la historia del repositorio se revisa.

## 1. Objetivo de la encuesta

Conocer las opiniones y expectativas de los consumidores adultos sobre la variedad y disponibilidad de productos en los supermercados, tomando a Tía como caso empresarial. Con esta información, se busca identificar posibles mejoras en el surtido y la reposición de productos que ayuden a orientar las decisiones de abastecimiento de la gerencia.

## 2. Población objetivo

- **Población:** Personas de 18 años o más que compran en supermercados al menos una vez al mes y que residen en Quito, Atuntaqui o Cuenca.

- **Límites y justificación:** La encuesta está dirigida a personas adultas que compran habitualmente en supermercados, ya que pueden compartir sus experiencias y opiniones sobre la variedad y disponibilidad de los productos. Se consideran Quito, Atuntaqui y Cuenca porque son las ciudades donde Tía tiene al menos una sucursal.  
No participarán menores de 18 años ni personas que compren en supermercados con una frecuencia menor a una vez al mes. Además, se trabajará con personas a las que los integrantes del equipo puedan contactar durante el laboratorio y que acepten responder voluntariamente.  
Las preguntas se plantearán tomando como referencia la situación actual de los mercados Tía respecto al tema de variedad y stock, y las opiniones de los encuestados sobre la variedad y disponibilidad de productos en los supermercados.

## 3. Método de muestreo

- **Método:** Muestreo estratificado por ciudad.

- **Tamaño y justificación:** El equipo se propone reunir 25 respuestas reales, con cinco participantes asignados a cada uno de los cinco integrantes. Esta cantidad está dentro del rango de 15 a 30 respuestas solicitado en el laboratorio y permitirá conocer las opiniones y expectativas de los participantes mediante un análisis descriptivo.
Simularemos el mismo número de registros recolectados por cada estudiante, asi obtendremos 50 registros totales.

- **Cómo se seleccionarán los participantes:** Cada integrante invitará a participar a familiares, amigos, compañeros u otras personas conocidas que cumplan con los requisitos establecidos. También se podrá pedir a quienes respondan la encuesta que compartan la invitación con otras personas que cumplan los mismos criterios.  
La participación será voluntaria y cada integrante procurará conseguir cinco respuestas válidas. De esta manera, el equipo podrá alcanzar la meta propuesta utilizando los contactos disponibles.<br>Se eligió este método porque el equipo puede contactar directamente a los participantes sin necesidad de disponer de un listado completo de consumidores para seleccionarlos al azar. Sin embargo, como las personas serán elegidas por su accesibilidad y por las recomendaciones de otros participantes, es posible que sus opiniones no representen las de todos los consumidores.  
Por esta razón, los resultados se utilizarán para describir las respuestas obtenidas, sin generalizarlos estadísticamente a toda la población.  
  

- **Equivalente en código (Python):** El siguiente código permite organizar la meta de respuestas de cada integrante y comprobar cuántas respuestas se espera reunir. La selección de los participantes se realizará mediante invitaciones directas y referidos, no mediante un sorteo aleatorio..

```python
import pandas as pd

df = pd.read_csv("encuestados.csv")

muestra = df.groupby("ciudad", group_keys=False).apply(
    lambda x: x.sample(frac=0.2, random_state=4)
)

print(muestra)
```

**Resultado esperado:** Se mostrará una tabla con los cinco integrantes y una meta de cinco 
respuestas para cada uno, lo que suma un total de 25 respuestas previstas. Este resultado 
corresponde a la planificación del equipo y no significa que los participantes ya hayan sido 
seleccionados o que las respuestas se hayan recopilado.

**Justificación del método:** El muestreo por conveniencia estructurado por estratos (ciudades) 
permite al equipo recolectar las respuestas de manera factible. Sin embargo, no elimina el sesgo 
de selección, por lo que los resultados no serán generalizables estadísticamente a toda la 
población y solo se utilizarán con fines descriptivos.

## 4. Cuestionario (5–10 preguntas)

Las preguntas buscan conocer los hábitos de compra de los participantes y sus opiniones sobre la variedad y disponibilidad de productos. 


| #  | Pregunta                                                                                                                                                                               | Tipo de variable   | Dtype al cargar | Opciones / escala                                                                                                       |
|----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| 1  | ¿En qué rango de edad se encuentra?                                                                                                                                                          | Categórica ordinal | `object`        |Menor de 18 años; 18 a 25 años; 26 a 35 años; 36 a 50 años; 51 a 65 años; Más de 65 años                                                                                                                 |
| 2  | ¿Con qué frecuencia compra en Almacenes Tía?                                                                                                                                          | Categórica ordinal | `object`        | Varias veces por semana; Una vez por semana; De 2 a 3 veces al mes; Una vez al mes; Una vez cada tres meses      |
| 3  | ¿En cuál de estas ciudades realiza habitualmente sus compras en Tía?                                                                                                                                                    | Categórica nominal | `object`        | Quito; Atuntaqui; Ambato                                                                                               |
| 4  | ¿Cómo califica la variedad de productos que encuentra habitualmente en Tía?                                                                                       | Categórica ordinal | `object`        | Muy insatisfecho/a; Insatisfecho/a; Ni satisfecho/a ni insatisfecho/a; Satisfecho/a; Muy satisfecho/a                                  |
| 5  | ¿Considera que Tía ofrece suficiente variedad de marcas y opciones para satisfacer sus necesidades?                                                                         | Categórica ordinal | `object`        | Totalmente en desacuerdo; En desacuerdo; Ni de acuerdo ni en desacuerdo; De acuerdo; Totalmente de acuerdo                                  |
| 6  | ¿Con qué frecuencia encuentra agotado un producto que desea comprar?                                                                       | Categórica ordinal | `object`        | Nunca; Casi nunca; Algunas veces; Casi siempre; Siempre                                                                 |
| 7  | Cuando encuentra un producto agotado, ¿con qué frecuencia consigue una alternativa adecuada dentro de la tienda?                                                                              | Categórica ordinal | `object`        |Nunca; Casi nunca; Algunas veces; Casi siempre; Siempre; No aplica |
| 8  | ¿Qué categoría de productos encuentra agotada con mayor frecuencia?                                                                                       | Categórica nominal | `object`        | Alimentos frescos; Productos empacados / Abarrotes; Bebidas; Productos de limpieza; Cuidado personal; Otra; No aplica                               |
| 9  | En general, ¿qué tan satisfecho/a está con la disponibilidad de productos en Tía?                                                                           | Categórica ordinal | `object`        | Muy insatisfecho/a; Insatisfecho/a; Ni satisfecho/a ni insatisfecho/a; Satisfecho/a; Muy satisfecho/a   |
| 10 | Cuando un producto que busca no está disponible, ¿qué acción suele tomar? | Categórica nominal | `object`        |Compro otra marca o presentación en Tía; Vuelvo otro día a Tía; Compro el producto en otro establecimiento; Cancelo la compra y no busco sustituto                                |


## 5. Análisis de sesgos

| Sesgo potencial                                                                                                                                                                                                                               | Mitigación                                                                                                                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1. Sesgo de selección:** Al reclutar a los encuestados entre familiares, amigos y conocidos de los 5 integrantes en Quito, Atuntaqui y Cuenca, la muestra no es aleatoria y puede sobrerepresentar a un perfil sociodemográfico específico. | Fijar cuotas explícitas por integrante para distribuir la encuesta entre diferentes rangos de edad y asegurar que se cumpla la cuota geográfica equitativa por ciudad. Asimismo, aclarar explícitamente en el reporte que los resultados son descriptivos y no inferenciales.                      |
| **2. Sesgo de deseabilidad social y preguntas hipotéticas:** Las preguntas 8 y 9 evalúan un escenario hipotético, esto suele llevar a los encuestados a responder de forma positiva o complaciente sin reflejar su comportamiento real.       | Redactar al inicio de esa sección un mensaje aclarando que la encuesta es totalmente **anónima** y que no existen respuestas _"correctas"_ o _"esperadas"._ Además, usar la pregunta 6 (frecuencia real de disponibilidad) para contrastar lo que el usuario experimenta frente a lo que desearía. |

## 6. Confidencialidad (RA3)
Los únicos datos personales que se solicitarán a los participantes son los siguientes:

 - **Nombres y apellidos:** Para llevar un control interno de la muestra y evitar duplicidad de respuestas.
- **Correo electrónico:** Como mecanismo de validación, dado que la encuesta se administrará a través de formularios en línea.
- **Ciudad de residencia:** Para comprobar que los encuestados pertenecen a una de las tres ciudades de interés definidas en el caso de estudio.


Para proteger la privacidad de los participantes en el estudio y cumplir con el tratamiento ético de los datos antes de realizar la exportación de los mismos a un archivo CSV. Se realizaran las siguientes acciones:

- 1.- Se eliminara la columna con los nombres y apellidos de los participantes y se les aignara un código id  unico a cada fila por ejemplo C_001.


- 2.- Se eliminara los correos electrónicos del CSV final dado que este unicámente es un requisito para poder llenar una encuesta vía internet usando herramientas como GoogleForms.



## 7. Verificación con herramientas (Python/R)

*Escribe `scripts/verificacion_encuesta.py` (o `.R`): debe cargar `plantillas/encuesta_respuestas.csv` y reportar los tipos de cada columna, los datos faltantes por columna y la distribución de `satisfaccion_general` y `recomendaria`. Incluye la salida y responde:*


``` python
import pandas as pd

archivo = "plantillas/encuesta_respuestas.csv"
df = pd.read_csv(archivo)

print("TIPOS DE DATOS POR COLUMNA")
print(df.dtypes)

print("\nDATOS FALTANTES POR COLUMNA")
print(df.isnull().sum())
```

- ¿Coinciden los tipos con tu predicción de la sección 4?
- ¿Cuántos datos faltantes hay por columna?

*Ejecuta el script sobre el CSV final (separa con un filtro de la columna `origen` las filas reales de las simuladas): ¿qué resultado delataría un sesgo de **no respuesta** y cuál un sesgo de **respuesta**? Escribe tu interpretación usando solo las respuestas reales.*
