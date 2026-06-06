# Geometría de los Mínimos Cuadrados Ordinarios (MCO) y Teorema FWL en ℝ³ 📊📐

Este repositorio contiene una aproximación didáctica y puramente geométrica a la estimación por Mínimos Cuadrados Ordinarios (MCO) y al **Teorema de Frisch-Waugh-Lovell (FWL)**, utilizando un espacio vectorial de tres dimensiones ($ℝ^3$) y visualizaciones interactivas en 3D. 

A diferencia de los enfoques estadísticos tradicionales, este proyecto prescinde temporalmente de los supuestos estocásticos de los estimadores para concentrarse en las **propiedades algebraicas y de proyección ortogonal** sobre subespacios lineales (colspace).

---

## 🔬 Datos y Enfoque Metodológico

Para poblar el espacio en $ℝ^3$, el script utiliza microdatos reales de la **Encuesta Nacional de Calidad de Vida (ENCV)** aplicada en el departamento del **Valle del Cauca, Colombia**.

### Variables Utilizadas:
- **$y$**: Logaritmo del ingreso o gasto declarado (Variable dependiente).
- **$v_1$**: Logaritmo del ingreso per cápita del hogar.
- **$v_2$**: Cantidad de personas en el hogar.

> **Nota Didáctica de Replicabilidad:** El algoritmo de limpieza aplica un bucle de muestreo aleatorio controlado (`set.seed(123)`) enfocado en extraer exactamente **3 observaciones** linealmente independientes. Esto asegura que los vectores tengan una varianza adecuada y que el ángulo entre regresores ($v_1$ y $v_2$) no genere multicolinealidad perfecta, permitiendo una representación clara en gráficos de tres ejes.

---

## 🛠️ Estructura del Proyecto e Intuición Analítica

El código está estructurado en módulos secuenciales dentro del reporte dinámico (`FWL_Simulacion.Rmd`):

1. **Unión de Microdatos:** Consolidación de 5 componentes sectoriales de la encuesta (Hogar, Vivienda, Salud, Composición y Servicios) indexados mediante la llave primaria `DIRECTORIO`.
2. **Filtrado y Centrado:** Extracción de la muestra del Valle del Cauca y cálculo de desvíos respecto a la media para proyectar los vectores directamente desde el origen $(0,0,0)$.
3. **Validación de Ortogonalidad:** Comprobación empírica de que el residuo es ortogonal al subespacio de los regresores mediante productos puntos equivalentes a cero:
   $$v_1^T e_1 \approx 0 \quad \text{y} \quad v_2^T e_2 \approx 0$$
4. **Visualización en Tres Dimensiones:** Implementación de gráficos interactivos usando la librería `plotly` en R:
   - **Doble Proyección 1D:** Visualiza de forma independiente las rectas que expanden ($span\{v_1\}$ y $span\{v_2\}$).
   - **Teorema FWL (Frisch-Waugh-Lovell):** Demostración gráfica de cómo parcializar el efecto de variables omitidas a través de las matrices de proyección ortogonal $M_1$ y $M_2$, aislando los residuos $M_1y$ sobre $M_1v_2$.
   - **Regresión Múltiple:** Renderizado del plano vectorial generado por los regresores y el vector proyectado de valores estimados $\hat{y}$.

---

## 💻 Requisitos y Tecnologías Utilizadas

Para interactuar con el modelo y renderizar el reporte HTML con el tema *Darkly*, es necesario contar con un entorno de R con las siguientes especificaciones:

- **R version 4.0+**
- **Librerías principales:** - `dplyr` (Manipulación de datos estructurados).
  - `plotly` (Renderizado interactivo de objetos vectoriales en 3D).
  - `rmarkdown` / `knitr` (Compilación del reporte).

### Instrucciones de Ejecución:
1. Asegúrate de modificar la variable `ruta` en el script con la dirección local donde almacenes los archivos `.CSV` de la ENCV.
2. Abre el archivo `FWL_Simulacion.Rmd` en RStudio.
3. Presiona el comando `Knit` (`Ctrl + Shift + K`) para compilar el archivo y abrir el lienzo interactivo en 3D en tu navegador.
