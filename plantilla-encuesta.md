# Plantilla de diseño — Encuesta de satisfacción (hito 1)

**Equipo:** Grupo 5

**Integrantes:** Ganchala Pavel, Lamiña Matias, Magarisca Bryan, Martínez Domenica, Medina Juan

**Fecha:** 20/10/2026

**Repositorio (fork):** [https://github.com/matiasLam67/IDSD422-lab2-diseno-encuesta-grupo-5.git](https://github.com/matiasLam67/IDSD422-lab2-diseno-encuesta-grupo-5.git)

**Enfoque del equipo (aprobado en clase):** Variedad y stock: satisfacción y disponibilidad.

Completa cada sección. Usa commits por sección; la historia del repositorio se revisa.

## 1. Objetivo de la encuesta

Estimar, dentro de la muestra, la proporción de compradores de RetailAndina en Quito, Guayaquil y Cuenca que califican con «Satisfecho/a» o «Muy satisfecho/a» la variedad y disponibilidad de productos, así como identificar las categorías con mayor frecuencia de quiebre de stock y la acción tomada ante un producto agotado. Estos resultados orientarán la decisión de gerencia para priorizar la reposición de inventario y ampliar el surtido en las categorías críticas durante el siguiente ciclo operativo.

## 2. Población objetivo

- **Población:** Personas mayores de edad (18 años o más) residentes en las zonas urbanas de Quito, Guayaquil o Cuenca que realizan compras en supermercados y tienen vínculo o experiencia de compra en RetailAndina.
- **Inclusión:** Tener 18 años o más, residir o comprar habitualmente en Quito, Guayaquil o Cuenca y responder el cuestionario completo según su frecuencia de compra.
- **Exclusión:** Menores de 18 años y personas residentes en otras ciudades fuera del alcance comercial del estudio. *(Nota: quienes responden «Nunca o no compro en RetailAndina» en la pregunta 2 finalizan la sección operativa de tienda y conservan valores `NaN` en las preguntas 3 a 10 por salto lógico del cuestionario).*

### Límites del estudio

- **Geográfico:** Ciudades principales de Quito, Guayaquil y Cuenca; se excluyen otras localidades para mantener comparables las plazas comerciales de la cadena.
- **Demográfico:** Personas desde los 18 años en adelante (segmentadas en rangos etarios desde 18–25 hasta más de 65 años) con autonomía de decisión de compra.
- **Comercial:** Compradores activos de RetailAndina para evaluar variedad, marcas, quiebres de stock y disponibilidad; se mantiene el registro de no compradores en la pregunta de frecuencia para dimensionar el alcance comercial.
- **Temporal:** Percepción y hábitos declarados al momento de responder, durante noviembre de 2026.

### Justificación

Delimitar la población a personas mayores de 18 años en Quito, Guayaquil y Cuenca permite evaluar el desempeño de surtido y reposición en las tres principales plazas urbanas del país sin sesgar las métricas de tienda con opiniones de personas que nunca compran en la cadena.


## 3. Método de muestreo

- **Método:** Muestreo no probabilístico por conveniencia con difusión por referidos en canales digitales (bola de nieve). Se contactó a personas accesibles de la red de los integrantes y se aplicó un salto lógico para separar a los compradores activos de quienes no compran en RetailAndina. Este método permite reunir la cuota de 15 a 30 respuestas reales exigida por la práctica, pero no permite generalizar estadísticamente los resultados a toda la población de las tres ciudades; dicha limitación se declara explícitamente en este informe.
- **Tamaño y justificación:** Se recolectaron **31 respuestas reales** (`origen = 'real'`), superando el mínimo de 15 a 30 respuestas exigido; de ellas, **25** corresponden a compradores activos de RetailAndina y **6** declararon «Nunca o no compro en RetailAndina». Para alcanzar el volumen de práctica (entre 60 y 100 filas) sin confundir datos sintéticos con evidencia de campo, se generaron **49 registros simulados** con semilla fija (`seed = 42`), marcados con `origen = 'simulada'`, totalizando **80 filas** en `plantillas/encuesta_respuestas.csv`.
- **No respuesta:** Se invitó a  personas de la red de contactos del equipo y se obtuvieron **6 respuestas nulas**, debido a que eran menores de edad y no compraban en RetailAndina.
- **Cómo se seleccionarán los participantes:** Cada integrante difundió el enlace del formulario entre familiares, amigos y conocidos mayores de 18 años en Quito, Guayaquil y Cuenca, procurando diversidad de rangos de edad y frecuencia de compra.


```python
import pandas as pd

respuestas = pd.read_csv("plantillas/encuesta_respuestas.csv")
elegibles = respuestas.query(
    "origen == 'real' and frecuencia_compra != 'Nunca o no compro en RetailAndina'"
)
muestra = elegibles.sample(
    n=min(25, len(elegibles)),
    random_state=42,
)
print(muestra[["id_respondente", "edad", "ciudad", "frecuencia_compra"]])
```

### Salida de la corrida

| Índice | id_respondente | edad | ciudad | frecuencia_compra |
|---:|:---|:---|:---|:---|
| 12 | R013 | 26 a 35 años | Cuenca | Una vez por semana |
| 22 | R023 | 18 a 25 años | Quito | Una vez por semana |
| 0 | R001 | 18 a 25 años | Quito | Varias veces por semana |
| 29 | R030 | 18 a 25 años | Quito | Una vez por semana |
| 15 | R016 | 26 a 35 años | Cuenca | Una vez al mes |
| 13 | R014 | 26 a 35 años | Cuenca | Una vez por semana |
| 18 | R019 | 18 a 25 años | Quito | Una vez por semana |
| 1 | R002 | 18 a 25 años | Quito | Varias veces por semana |
| 28 | R029 | 36 a 50 años | Quito | Una vez al mes |
| 7 | R008 | 18 a 25 años | Cuenca | Varias veces por semana |
| 2 | R003 | 18 a 25 años | Quito | Una vez al mes |
| 16 | R017 | 18 a 25 años | Quito | Una vez al mes |
| 20 | R021 | 18 a 25 años | Quito | Una vez por semana |
| 5 | R006 | 36 a 50 años | Quito | Varias veces por semana |
| 6 | R007 | 36 a 50 años | Quito | De 2 a 3 veces al mes |
| 26 | R027 | 26 a 35 años | Guayaquil | Una vez por semana |
| 23 | R024 | 18 a 25 años | Quito | De 2 a 3 veces al mes |
| 27 | R028 | 26 a 35 años | Quito | Una vez por semana |
| 24 | R025 | 51 a 65 años | Quito | Una vez al mes |
| 30 | R031 | 36 a 50 años | Quito | Una vez al mes |
| 10 | R011 | 18 a 25 años | Cuenca | De 2 a 3 veces al mes |
| 14 | R015 | 18 a 25 años | Cuenca | Una vez por semana |
| 19 | R020 | 36 a 50 años | Quito | Una vez por semana |
| 25 | R026 | 26 a 35 años | Quito | De 2 a 3 veces al mes |
| 9 | R010 | 26 a 35 años | Cuenca | Varias veces por semana |

Como existen 25 compradores activos reales elegibles (`origen == 'real'`), `sample()` selecciona de forma reproducible los 25 registros fijando el orden mediante `random_state=42`. No constituye un muestreo probabilístico de toda la población urbana, por lo que los hallazgos se interpretan de manera descriptiva sobre la muestra recolectada.

## 4. Cuestionario (10 preguntas)

El cuestionario consta de 10 preguntas cerradas, neutras y específica, una idea por pregunta, conservando exactamente las mismas opciones aplicadas en el formulario. La pregunta 1 y 2 actúa como salto lógico: quienes responden «Menor de 18 años» y/o «Nunca o no compro en RetailAndina» no responden las preguntas 3 a 10 (registrándose como `NaN` en el CSV).

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


| Sesgo potencial | Cómo podría aparecer | Mitigación |
| :--- | :--- | :--- |
| **Sesgo de selección** | Al difundir el formulario entre conocidos del equipo,se sobrerrepresentan jóvenes de 18 a 25 años (17 de 31 reales, 54.8 %) y compradores de Quito (17 de 25 compradores reales, 68.0 %), frente a una menor participación en Cuenca (7) y Guayaquil (1). | Ampliar la difusión mediante referidos en Guayaquily Cuenca y en rangos mayores de 25 años, declarar explícitamente que el muestreo es no probabilístico por conveniencia y reportar resultados desagregados solo sobre origen == 'real'. |
| **Sesgo de respuesta** | Los encuestados cercanos al equipo pueden tender a otorgar calificaciones favorables por cortesía, o recordar con mayor facilidad episodios puntuales de quiebre de stock reciente. | Garantizar anonimato total (sin solicitar nombre ni correo), emplear redacción neutral con escalas Likert balanceadas de 5 puntos incluyendo punto neutro y enfocar las preguntas en hábitos habituales. |


### Evidencia en las respuestas reales (`n = 31` totales; `n = 25` compradores activos)

* **Satisfacción general:** Entre los 25 compradores reales activos, el **72.0 %** (18/25) calificó con «Satisfecho/a» (52.0 %) o «Muy satisfecho/a» (20.0 %) la variedad de productos, y el **76.0 %** (19/25) calificó positivamente la disponibilidad (60.0 % «Satisfecho/a» y 16.0 % «Muy satisfecho/a»).
* **Comportamiento ante quiebres de stock:** Sin embargo, el **52.0 %** (13/25) afirmó que, cuando un producto no está disponible, compra el producto en otro establecimiento, concentrándose los quiebres reportados en **Alimentos frescos** (8/25, 32.0 %) y **Cuidado personal** (6/25, 24.0 %).
* **Nota metodológica:** Las 49 filas simuladas (`origen = 'simulada'`) fueron generadas únicamente para completar el volumen muestral de práctica (80 filas en total) y no se utilizan para extraer conclusiones sobre sesgos ni comportamiento real de los clientes.


## 6. Confidencialidad (RA3)
### Protección de datos y anonimización

* **Datos personales que se piden y por qué:** Únicamente se almacenan el rango de edad (`edad`), la frecuencia de compra (`frecuencia_compra`) y la ciudad habitual de compra (`ciudad`), necesarios para segmentar el perfil del comprador y contextualizar las plazas comerciales. No se solicitan nombres, apellidos, cédulas, teléfonos, correos electrónicos, direcciones exactas ni datos financieros.

* **Plan de anonimización:** Se eliminó la columna `Marca temporal` del formulario original para evitar trazabilidad por hora de envío. Cada registro real recibió un código secuencial anónimo (`R001` a `R031`) y cada registro simulado recibió un código (`S001` a `S049`), diferenciados mediante la columna `origen` (`real` / `simulada`). El archivo crudo exportado desde Google Forms no se sube al repositorio; únicamente se publica el archivo limpio y anonimizado en `plantillas/encuesta_respuestas.csv`.


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
