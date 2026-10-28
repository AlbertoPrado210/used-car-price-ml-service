# Fuente de datos

## Conjunto seleccionado

- **Nombre:** DVM-CAR 2.0
- **Versión utilizada:** 2.0
- **Responsables:** Jingmin Huang, Bowei Chen, Lan Luo, Shigang Yue e Iadh Ounis
- **Mercado representado:** Reino Unido
- **Tipo de observación:** anuncio individual de vehículo usado
- **Fuente oficial:** https://deepvisualmarketing.github.io/
- **Registro persistente:** https://doi.org/10.6084/m9.figshare.19586296
- **Licencia declarada:** Creative Commons Attribution-NonCommercial 4.0 International, CC BY-NC 4.0
- **Fecha local de descarga y verificación:** 28 de octubre de 2026

La licencia permite el uso y la adaptación con atribución para fines no comerciales. Este proyecto se desarrolla como ejercicio educativo y demostración de capacidades. Los archivos originales no se redistribuirán mediante el repositorio Git.

## Archivo principal

El análisis utilizará `data/raw/dvm_car_v2/Ad_table (extra).csv` como fuente principal.

El archivo contiene los mismos 268 255 identificadores de anuncio que `Ad_table.csv` y conserva los mismos valores numéricos de precio. Añade las siguientes variables:

- `Engine_power`
- `Annual_Tax`
- `Wheelbase`
- `Height`
- `Width`
- `Length`
- `Average_mpg`
- `Top_speed`

Los espacios iniciales presentes en dos encabezados del archivo enriquecido forman parte de la fuente original. Se corregirán únicamente en una representación procesada, sin modificar el archivo ubicado en `data/raw/`.

## Integridad de la descarga

- **Archivo ZIP:** `tables_V2.0.zip`
- **SHA-256 del ZIP:** `aff96174816825d5009ac810cffeb6f878fe7295adf1df4c2f922232fcf19f39`
- **SHA-256 de `Ad_table (extra).csv`:** `0211abfe049d247bf42ad09bff968de6c81e2c810d6b026e4385ff5cbbbac476`
- **Filas del archivo principal:** 268 255
- **Columnas del archivo principal:** 24
- **Delimitador:** coma
- **Lectura verificada:** compatible con UTF-8

Las huellas de los siete archivos CSV extraídos coinciden con las de sus contenidos dentro del ZIP descargado.

## Variable objetivo provisional

La variable `Price` se utilizará provisionalmente como precio anunciado. Aunque la documentación del conjunto emplea la expresión *selling price*, la unidad de observación es un anuncio y no existe evidencia proporcionada de que cada precio corresponda a una transacción completada.

[No Verificado] La moneda no está codificada en el archivo ni se declara explícitamente en el manual o en el artículo consultado. No se etiquetará como GBP hasta encontrar evidencia documental suficiente.

## Hallazgos iniciales de integridad

Estos resultados proceden de una inspección de solo lectura. Todavía no constituyen decisiones de limpieza.

- No se detectaron filas completamente duplicadas.
- `Adv_ID` no presenta duplicados ni valores faltantes.
- `Price` contiene 1 145 valores faltantes, equivalentes al 0,427 % de las observaciones.
- Los precios no faltantes se encuentran entre 100 y 9 999 999.
- El precio mediano es 9 299 y el percentil 99 es 92 989,91.
- `Adv_year` contiene años entre 2012 y 2021.
- `Reg_year` contiene valores entre 1900 y 2019, además de siete valores faltantes.
- `Adv_month` presenta 15 valores distintos y un máximo de 33. No debe interpretarse todavía como mes calendario sin revisar su codificación.
- Varias variables con significado numérico fueron leídas como texto, entre ellas `Runned_Miles`, `Engin_size`, `Annual_Tax`, `Average_mpg` y `Top_speed`.

Los valores extremos, formatos de texto, faltantes y posibles reglas de dominio se investigarán antes de eliminar, imputar o transformar observaciones.

## Referencia

Huang, J., Chen, B., Luo, L., Yue, S., & Ounis, I. (2022). DVM-CAR: A large-scale automotive dataset for visual marketing research and applications. *2022 IEEE International Conference on Big Data (Big Data)*, 4140–4147. https://doi.org/10.1109/BigData55660.2022.10020634
