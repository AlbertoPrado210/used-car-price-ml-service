# Definición del proyecto

## Identificación

- **Nombre de trabajo:** `used-car-price-ml-service`
- **Tipo de proyecto:** servicio de aprendizaje automático para regresión
- **Fecha de definición inicial:** 15 de octubre de 2026
- **Estado:** alcance inicial aprobado

## 1. Planteamiento del problema

El responsable del inventario de un concesionario necesita estimar un precio de referencia para vehículos usados a partir de sus características observables. El proyecto desarrollará un servicio que produzca una estimación puntual y un rango orientativo, con un proceso de entrenamiento reproducible y una evaluación explícita de sus errores y limitaciones.

El resultado apoyará la decisión de establecer un precio inicial de publicación y permitirá detectar vehículos cuyo precio anunciado se aleje de la estimación generada por el modelo.

## 2. Usuario objetivo

El usuario principal será el responsable del inventario del concesionario, quien también actuará como responsable funcional del proyecto.

Como usuarios secundarios se consideran:

- vendedores particulares que necesiten una referencia inicial;
- compradores que deseen contrastar un precio anunciado.

Estos usuarios secundarios no definirán los requisitos de la primera versión.

## 3. Resultado esperado

Para cada vehículo aceptado por el servicio se devolverán:

1. una estimación puntual del precio;
2. un límite inferior orientativo;
3. un límite superior orientativo.

El rango se diseñará como un intervalo de predicción con cobertura nominal del 90 %. Su cobertura empírica y su amplitud deberán evaluarse sobre observaciones no utilizadas para ajustar el modelo ni para calibrar el intervalo.

El intervalo no se interpretará como una garantía del precio final ni como un intervalo de confianza para la media.

## 4. Variable objetivo

La variable objetivo provisional será el precio anunciado del vehículo.

Esta definición solo se cambiará a precio de venta si la fuente de datos acredita que sus observaciones corresponden a transacciones completadas. La procedencia, licencia, moneda, mercado geográfico y periodo de observación todavía no han sido verificados y deberán resolverse antes de utilizar datos.

## 5. Alcance inicial

### 5.1 Incluido

- Predicción para vehículos usados pertenecientes al mercado y periodo que posteriormente se verifiquen en la fuente de datos.
- Uso exclusivo de variables disponibles antes de publicar o valorar el vehículo.
- Entrenamiento reproducible.
- Comparación con una línea base mediante `DummyRegressor`.
- Separación de datos antes de aprender transformaciones.
- Preprocesamiento y modelo integrados en una única canalización.
- Evaluación global y por segmentos relevantes.
- Presentación de MAE y RMSE en la unidad monetaria de la variable objetivo.
- Evaluación de R² como medida complementaria.
- Evaluación de la cobertura y amplitud del intervalo de predicción.
- API para predicciones individuales con validación explícita de entradas.
- Pruebas automatizadas y documentación técnica.

### 5.2 Excluido de la primera versión

- Vehículos nuevos.
- Análisis de imágenes.
- Procesamiento de descripciones en texto libre.
- Uso de historiales de accidentes o mantenimiento que no estén presentes en la fuente de datos.
- Conversión dinámica entre monedas.
- Consulta o extracción de anuncios externos en tiempo real.
- Recomendaciones automáticas de compra o financiamiento.
- Tasaciones oficiales o garantías sobre el precio final de venta.

## 6. Criterios verificables de éxito

La primera versión se considerará técnicamente satisfactoria cuando cumpla conjuntamente los siguientes criterios:

1. El modelo final obtiene un MAE inferior al de `DummyRegressor` mediante validación cruzada en los datos de entrenamiento.
2. El modelo final obtiene un MAE inferior al de `DummyRegressor` en un conjunto de prueba reservado.
3. MAE y RMSE se informan en la moneda original de la variable objetivo.
4. El conjunto de prueba se separa antes de ajustar imputadores, codificadores, escaladores, selectores o modelos.
5. El preprocesamiento y el estimador se almacenan como una única canalización reproducible.
6. La cobertura empírica del intervalo se informa sobre datos independientes de su entrenamiento y calibración, junto con su amplitud promedio.
7. Las predicciones de la API reproducen las obtenidas mediante la canalización evaluada.
8. Las entradas inválidas son rechazadas mediante esquemas explícitos y pruebas automatizadas.
9. Se documentan la procedencia, la licencia, la población representada, el periodo, los supuestos y las limitaciones de los datos.
10. El error se analiza tanto globalmente como en segmentos relevantes definidos antes de la evaluación final.

No se establece todavía un umbral monetario máximo para MAE o RMSE. Dicho umbral requiere conocer la moneda, la distribución de precios, la variabilidad y el contexto comercial de la fuente seleccionada.

## 7. Decisiones pendientes

Antes de iniciar el análisis o el entrenamiento deberán resolverse y documentarse:

- fuente y licencia del conjunto de datos;
- naturaleza del precio registrado, anuncio o transacción;
- país o mercado representado;
- moneda y periodo temporal;
- unidad de observación y posibles duplicados;
- variables disponibles en el momento de la predicción;
- método de partición apropiado según la estructura temporal y grupal de los datos;
- procedimiento de construcción y calibración del intervalo de predicción.

## 8. Restricciones de interpretación

El servicio proporcionará una referencia estadística basada en la población representada por los datos. No sustituirá una inspección física, una tasación profesional ni una evaluación del estado mecánico del vehículo.

La posibilidad de generalizar las predicciones a otros mercados, monedas o periodos deberá demostrarse empíricamente. Hasta entonces, no se asumirá que el modelo es válido fuera del dominio observado.
