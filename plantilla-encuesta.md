# Plantilla de diseño — Encuesta de satisfacción (hito 1)

**Equipo:** Grupo 5

**Integrantes:** Ganchala Pavel, Lamiña Matias, Magarisca Bryan, Martínez Domenica, Medina Juan

**Fecha:** 19/11/2026

**Repositorio (fork):** [https://github.com/pavexl/IDSD422-lab2-diseno-encuesta-grupo-5](https://github.com/pavexl/IDSD422-lab2-diseno-encuesta-grupo-5)

**Enfoque del equipo (aprobado en clase):** Variedad y stock, satisfacción y disponibilidad.

## 1. Objetivo de la encuesta

Estimar, dentro de la muestra, la proporción de participantes que califican positivamente la variedad y disponibilidad de productos en supermercados, tomando a RetailAndina como un caso empresarial ficticio. Asimismo, identificar las categorías en las que los participantes reportan mayor frecuencia de productos agotados y las acciones que suelen tomar ante esa situación. Los resultados servirán como referencia descriptiva para orientar decisiones hipotéticas de surtido y reposición de inventario.

## 2. Población objetivo

- **Población:** Personas mayores de edad (18 años o más) que residen en las zonas urbanas de Quito, Guayaquil o Cuenca y realizan compras en supermercados al menos una vez al mes.

- **Límites y justificación:** El estudio se delimita geográficamente a las zonas urbanas de Quito, Guayaquil y Cuenca, Ecuador. Se consideran personas de 18 años o más que compran en supermercados al menos una vez al mes, porque pueden aportar experiencias sobre la variedad de productos, la disponibilidad y las situaciones de agotamiento de stock. RetailAndina se utiliza como un caso empresarial ficticio para contextualizar la encuesta; por tanto, no es necesario que los participantes sean clientes reales de dicha empresa. La información corresponde a las percepciones de los participantes en el momento de responder la encuesta, durante noviembre de 2026.

## 3. Método de muestreo

- **Método:** Muestreo no probabilístico por conveniencia y referencias (bola de nieve).

- **Tamaño y justificación:** Se recopilaron 31 respuestas reales, de las cuales 25 están completas en las preguntas de evaluación y 6 son parciales. Estas últimas corresponden a participantes que seleccionaron «Nunca o no compro en RetailAndina» en la pregunta 2, lo que activó la lógica de salto y dejó sin respuesta las preguntas 3 a 10. Se conservaron las seis respuestas parciales para mantener la integridad de los datos. Además, se incorporaron 44 registros simulados para fines académicos, identificados con `origen = simulada`. El archivo final contiene 75 registros: 31 reales y 44 simulados.

- **Cómo se seleccionaron los participantes:** El cuestionario se compartió con familiares, amigos, compañeros y conocidos de los integrantes del grupo. La participación fue voluntaria y dependió de la accesibilidad y disponibilidad de las personas. La captación se realizó mediante conveniencia y referencias, por lo que no todos los integrantes de la población tuvieron la misma probabilidad de participar. Los registros simulados que no cumplían los criterios de inclusión definidos para la práctica fueron retirados.

- **Equivalente en código (Python o R):** El reclutamiento se realizó por conveniencia y referencias, no mediante una selección aleatoria. El siguiente código permite identificar y seleccionar de forma reproducible las 25 respuestas reales completas para su revisión. Esta selección se realiza después de recopilar las respuestas y no representa el procedimiento original de reclutamiento.

```python
import pandas as pd

respuestas = pd.read_csv("plantillas/encuesta_respuestas.csv")

completas = respuestas[
    (respuestas["origen"] == "real") &
    (respuestas["frecuencia_compra"] != "Nunca o no compro en RetailAndina")
]

muestra = completas.sample(
    n=25,
    random_state=42
)

print(muestra["id_respondente"].tolist())
```

**Salida de una corrida:**

```text
['R013', 'R023', 'R001', 'R030', 'R016',
 'R014', 'R019', 'R002', 'R029', 'R008',
 'R003', 'R017', 'R021', 'R006', 'R007',
 'R027', 'R024', 'R028', 'R025', 'R031',
 'R011', 'R015', 'R020', 'R026', 'R010']
```

La semilla `random_state=42` permite reproducir el orden de selección. El resultado contiene 25 respuestas reales completas. Este procedimiento sirve para organizar y revisar los registros recopilados, pero no debe confundirse con el reclutamiento por conveniencia realizado durante la encuesta.

## 4. Cuestionario (10 preguntas)

El cuestionario consta de 10 preguntas cerradas, diseñadas para recopilar información sobre la variedad de productos, su disponibilidad y la satisfacción de los participantes. Se conserva la redacción y las opciones originales utilizadas en el formulario aplicado. Las preguntas 1 y 2 incluyen una lógica de salto: quienes seleccionan «Menor de 18 años» en la primera pregunta o «Nunca o no compro en RetailAndina» en la segunda finalizan el cuestionario y no responden las preguntas 3 a 10. Estas respuestas posteriores se registran como datos faltantes (`NaN`) en el CSV.

**Limitación del instrumento:** Aunque las preguntas hacen referencia a RetailAndina, esta empresa es un caso ficticio. Los participantes fueron informados de esta condición y respondieron basándose en sus experiencias generales con supermercados. Por tanto, las respuestas representan percepciones generales y no experiencias verificadas de compra en RetailAndina.

| # | Variable | Pregunta | Tipo de variable | Dtype al cargar |
|---:|:---|:---|:---|:---|
| 1 | `edad` | ¿En qué rango de edad se encuentra? | Cualitativa ordinal | `object` |
| 2 | `frecuencia_compra` | ¿Con qué frecuencia compra en RetailAndina? | Cualitativa ordinal | `object` |
| 3 | `ciudad` | ¿En cuál de estas ciudades realiza habitualmente sus compras en RetailAndina? | Cualitativa nominal | `object` |
| 4 | `satisfaccion_variedad` | ¿Qué tan satisfecho/a está con la variedad de productos que encuentra en RetailAndina? | Cualitativa ordinal | `object` |
| 5 | `suficiente_variedad_marcas` | ¿Considera que RetailAndina ofrece suficiente variedad de marcas y opciones para satisfacer sus necesidades? | Cualitativa ordinal | `object` |
| 6 | `frecuencia_agotado` | ¿Con qué frecuencia encuentra agotado un producto que desea comprar en RetailAndina? | Cualitativa ordinal | `object` |
| 7 | `alternativa_agotado` | Cuando encuentra un producto agotado, ¿con qué frecuencia consigue una alternativa adecuada dentro de la tienda? | Cualitativa ordinal | `object` |
| 8 | `categoria_agotada` | ¿Qué categoría de productos encuentra agotada con mayor frecuencia en RetailAndina? | Cualitativa nominal | `object` |
| 9 | `satisfaccion_disponibilidad` | En general, ¿qué tan satisfecho/a está con la disponibilidad de productos en RetailAndina? | Cualitativa ordinal | `object` |
| 10 | `accion_producto_no_disponible` | Cuando un producto que busca no está disponible en RetailAndina, ¿qué acción suele tomar? | Cualitativa nominal | `object` |

### Detalle del formulario aplicado

1. **Edad (`edad`):** ¿En qué rango de edad se encuentra?
   - Menor de 18 años / 18 a 25 años / 26 a 35 años / 36 a 50 años / 51 a 65 años / Más de 65 años *(salto lógico: finaliza preguntas de experiencia en tienda)*
2. **Frecuencia de compra (`frecuencia_compra`):** ¿Con qué frecuencia compra en RetailAndina?
   - Varias veces por semana / Una vez por semana / De 2 a 3 veces al mes / Una vez al mes / Menos de una vez al mes / Nunca o no compro en RetailAndina *(salto lógico: finaliza preguntas de experiencia en tienda)*
3. **Ciudad habitual de compra (`ciudad`):** ¿En cuál de estas ciudades realiza habitualmente sus compras en RetailAndina?
   - Quito / Guayaquil / Cuenca
4. **Satisfacción con la variedad (`satisfaccion_variedad`):** ¿Qué tan satisfecho/a está con la variedad de productos que encuentra en RetailAndina?
   - Muy insatisfecho/a / Insatisfecho/a / Ni satisfecho/a ni insatisfecho/a / Satisfecho/a / Muy satisfecho/a
5. **Suficiencia de marcas y opciones (`suficiente_variedad_marcas`):** ¿Considera que RetailAndina ofrece suficiente variedad de marcas y opciones para satisfacer sus necesidades?
   - Totalmente en desacuerdo / En desacuerdo / Ni de acuerdo ni en desacuerdo / De acuerdo / Totalmente de acuerdo
6. **Frecuencia de productos agotados (`frecuencia_agotado`):** ¿Con qué frecuencia encuentra agotado un producto que desea comprar en RetailAndina?
   - Nunca / Casi nunca / Algunas veces / Casi siempre / Siempre
7. **Alternativa adecuada en tienda (`alternativa_agotado`):** Cuando encuentra un producto agotado, ¿con qué frecuencia consigue una alternativa adecuada dentro de la tienda?
   - Nunca / Casi nunca / Algunas veces / Casi siempre / Siempre / No aplica (nunca he encontrado un producto agotado)
8. **Categoría más agotada (`categoria_agotada`):** ¿Qué categoría de productos encuentra agotada con mayor frecuencia en RetailAndina?
   - Alimentos frescos / Productos empacados / Abarrotes / Bebidas / Productos de limpieza / Cuidado personal / Otra / No aplica
9. **Satisfacción general con la disponibilidad (`satisfaccion_disponibilidad`):** En general, ¿qué tan satisfecho/a está con la disponibilidad de productos en RetailAnd

## 5. Análisis de sesgos

| Sesgo potencial | Mitigación |
|---|---|
| **Sesgo de selección:** La encuesta se difundió entre familiares, amigos, compañeros y conocidos del equipo, por lo que puede existir una sobrerrepresentación de personas jóvenes de 18 a 25 años (17 de 31 respuestas reales, 54.8 %) y de participantes de Quito (17 de 25 respuestas reales completas, 68.0 %). La participación de Guayaquil fue menor (1 respuesta completa) y la de Cuenca fue de 7 respuestas completas. | Ampliar la difusión mediante contactos y referencias en las tres ciudades, especialmente entre los grupos de edad menos representados. Declarar que se utilizó un muestreo no probabilístico por conveniencia y referencias, y presentar los resultados como descriptivos de la muestra, sin generalizarlos a toda la población. |
| **Sesgo de respuesta:** Los participantes, al conocer a integrantes del equipo, podrían sentirse inclinados a dar calificaciones favorables por cortesía. Además, podrían recordar con mayor facilidad situaciones recientes de productos agotados. | Mantener la participación voluntaria, proteger la confidencialidad de los participantes, evitar solicitar datos identificativos en el archivo compartido y utilizar preguntas neutrales con escalas equilibradas que incluyan opciones positivas, negativas y neutras. |

### Evidencia en las respuestas reales

El análisis de las preguntas de evaluación se realiza únicamente con las 25 respuestas reales completas. Los resultados describen las experiencias generales de los participantes en supermercados, no la satisfacción de clientes reales de RetailAndina.

- **Satisfacción con la variedad:** 18 de 25 participantes (72.0 %) respondieron «Satisfecho/a» o «Muy satisfecho/a».
- **Satisfacción con la disponibilidad:** 19 de 25 participantes (76.0 %) respondieron «Satisfecho/a» o «Muy satisfecho/a».
- **Comportamiento ante productos no disponibles:** 13 de 25 participantes (52.0 %) indicaron que compran el producto en otro establecimiento.
- **Categorías con productos agotados:** las más mencionadas fueron alimentos frescos (8 de 25, 32.0 %) y cuidado personal (6 de 25, 24.0 %).

**Nota metodológica:** El archivo final contiene 44 registros simulados (`origen = simulada`), utilizados para practicar el procesamiento de datos. Estos registros no se consideran respuestas reales ni se utilizan para obtener las conclusiones anteriores. Los resultados presentados corresponden exclusivamente a las 25 respuestas reales completas. Las otras 6 respuestas reales se conservan como parciales y no se incluyen en los cálculos de satisfacción.

## 6. Confidencialidad (RA3)

### Protección de datos y anonimización

- **Datos personales que se piden y por qué:** Google Forms recopiló automáticamente las direcciones de correo electrónico de los participantes. Además, el cuestionario solicitó rangos de edad, frecuencia de compra y ciudad habitual de compra, con el propósito de describir las características generales de la muestra y contextualizar las respuestas. No se solicitaron nombres, apellidos, cédulas, teléfonos, direcciones exactas ni datos financieros.

- **Plan de anonimización:** Para compartir los resultados en el repositorio se excluyeron las direcciones de correo electrónico y la marca temporal del formulario. Cada respuesta real se identificó mediante un código secuencial (`R001` a `R031`) y cada registro simulado mediante un código (`S001` a `S044`), diferenciados por la columna `origen` (`real` / `simulada`). El archivo original exportado desde Google Forms, que contiene información identificativa, no se publica en el repositorio. Se comparte únicamente el archivo depurado `plantillas/encuesta_respuestas.csv`. El archivo original debe mantenerse con acceso restringido y utilizarse únicamente para los fines académicos del proyecto.

## 7. Verificación con herramientas (Python/R)

``` python
import pandas as pd

archivo = "plantillas/encuesta_respuestas.csv"
df = pd.read_csv(archivo)

print("TIPOS DE DATOS POR COLUMNA")
print(df.dtypes)

print("\nDATOS FALTANTES POR COLUMNA")
print(df.isnull().sum())
```
`El código que se muestra en la parte superior es un código temporal, esto debido a que para poder contestar las preguntas debemos realizar las encuestas y comparar con la sección por lo cual es solo un ejemplo general`

- ¿Coinciden los tipos con tu predicción de la sección 4?

- ¿Cuántos datos faltantes hay por columna? 

¿Qué resultado delataría un sesgo de **no respuesta** y cuál un sesgo de **respuesta**? Escribe tu interpretación usando solo las respuestas reales.
