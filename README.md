# Brecha Digital en México – ENDUTIH 2022

Análisis estadístico de la relación entre edad, sexo y tipo de celular
(smartphone / básico) en tres estados del sur de México (Chiapas, Guerrero
y Oaxaca), usando microdatos de la Encuesta Nacional sobre Disponibilidad y
Uso de Tecnologías de la Información en los Hogares (ENDUTIH) 2022.

## Estructura del repositorio

.
├── muestreo_aleatorio.ipynb        # Carga, limpieza, filtrado por estados y generación de submuestras
├── EDA.ipynb                       # Análisis exploratorio de datos (gráficos, descriptivos, asociaciones)
├── prueba_hipotesis.ipynb          # Pruebas de hipótesis (chi-cuadrado, z, t, análisis estratificado por sexo)
├── regresion_logistica.ipynb       # Modelo de regresión logística con interacción edad*sexo
├── factor_expansion.ipynb          # Estimaciones poblacionales usando el factor de expansión FAC_PER
├── submuestra1.csv                 # Submuestra aleatoria 1 (100 registros)
├── submuestra2.csv                 # Submuestra aleatoria 2 (100 registros)
├── submuestra3.csv                 # Submuestra aleatoria 3 (100 registros)
├── sub_hombres.csv                 # Registros de la muestra combinada correspondientes a hombres
├── sub_mujeres.csv                 # Registros de la muestra combinada correspondientes a mujeres
├── tr_endutih_usuarios2_anual_2022_mod.xlsx  # Archivo original de microdatos
├── diccionario_de_datos_tr_endutih_usuarios2_anual_2022.csv  # Archivo original de diccionario de datos
└── README.md

## Fuente

- **Encuesta:** ENDUTIH 2022 (Encuesta Nacional sobre Disponibilidad y Uso de Tecnologías
  de la Información en los Hogares).
- **Año:** 2022.
- **Módulo:** Usuarios 2 – Módulo de telefonía celular.
- **Archivo original:** `tr_endutih_usuarios2_anual_2022_mod.xlsx`.
- **Instituto:** INEGI (Instituto Nacional de Estadística y Geografía).

## Variables utilizadas

| Variable original | Descripción | Valores |
|-------------------|-------------|---------|
| `EDAD` | Edad del informante | 0 – 99 años |
| `P8_4_2` | ¿El celular que usa es smartphone? | 1 = Sí, 2 = No |
| `SEXO` | Sexo del informante | 1 = Hombre, 2 = Mujer |
| `ENT` | Entidad federativa | 7 = Chiapas, 12 = Guerrero, 20 = Oaxaca |
| `FAC_PER` | Factor de expansión poblacional | Peso que representa a cada individuo en la población |

## Transformaciones realizadas

- **Filtrado geográfico:** solo se conservaron los registros de Chiapas, Guerrero y Oaxaca (`ENT` 7, 12, 20).
- **Muestreo estratificado:** se extrajeron hasta 100 registros por estado (total aproximado de 300)
  con `random_state=42` para garantizar reproducibilidad.
- **Eliminación de nulos:** se descartaron filas con valores faltantes en `EDAD`, `P8_4_2`, `SEXO`, `ENT`.
- **Creación de variable categórica `edad_grupo`:** se agrupó la edad en 6 intervalos
  (<18, 18‑29, 30‑39, 40‑49, 50‑59, 60+).
- **Codificación binaria de la variable respuesta:** `smart` = 1 si `P8_4_2` = 1 (smartphone),
  0 en caso contrario.
- **Generación de submuestras:** la muestra combinada se dividió aleatoriamente en tres
  submuestras (`submuestra1.csv`, `submuestra2.csv`, `submuestra3.csv`).
- **Partición por sexo:** se crearon los archivos `sub_hombres.csv` y `sub_mujeres.csv`
  a partir de la columna `SEXO`.
- **Uso del factor de expansión:** se cargó la variable `FAC_PER` para obtener estimaciones
  poblacionales ponderadas (proporción de smartphone, intervalos de confianza).

## Preguntas de investigación

1. **Asociación:** ¿Existe relación entre la edad y el tipo de celular que usan los mexicanos?
2. **Comparación por sexo:** ¿La asociación entre edad y tipo de celular difiere entre hombres y mujeres?
3. **Regresión:** ¿Qué factores (edad y sexo) están asociados con la probabilidad de usar un
   smartphone y existe una interacción entre ellos?

## Métodos estadísticos aplicados

- Análisis exploratorio (histogramas, boxplots, tablas de contingencia, V de Cramér).
- Prueba chi‑cuadrado de independencia (α = 0.005).
- Prueba z para diferencia de proporciones (α = 0.05).
- Prueba t para diferencia de medias (α = 0.05), con verificación de supuestos
  (Shapiro‑Wilk, Levene).
- Análisis estratificado por sexo (comparación de V de Cramér).
- Regresión logística con interacción, razón de verosimilitud, pseudo‑R² de McFadden,
  AUC‑ROC, VIF, prueba de Hosmer‑Lemeshow.
- Estimaciones poblacionales ponderadas usando el factor de expansión `FAC_PER`.

## Requisitos

- Python 3.8 o superior.
- Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`,
  `scikit-learn`, `openpyxl`.
- El archivo `tr_endutih_usuarios2_anual_2022_mod.xlsx` se encuentra en la raíz del proyecto.

## Créditos

Proyecto desarrollado como parte de la materia **Estadística**.

**Estudiantes:**
- Hernández Martínez Pablo
- Reyes Calva Angel David

**Profesora:** Dra. Claudia García Blanquel  
**Grupo:** 4AM1  
**Escuela:** Escuela Superior de Cómputo (ESCOM)