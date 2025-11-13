# Tarea Evaluativa – Algoritmos de Optimización

Proyecto de curso para analizar y comparar algoritmos numéricos de optimización sobre una función objetivo específica. En el notebook se implementan y experimentan los siguientes métodos:

- Descenso por Gradiente (con búsqueda de línea tipo Armijo)
- Quasi-Newton BFGS (con Armijo)
- Método híbrido (GD lejos + conmutación a BFGS cuando \(\|x\|\le R_{\text{switch}}\))

La experimentación, visualizaciones y almacenamiento de resultados se realizan en la notebook `code/proyecto.ipynb`.

## Función objetivo

Sea $r = \sqrt{x² + y² + 1}:

$f(x, y) = -200 \exp{-0.02 r}$

Es una función radial, suave y con mínimo global en el origen (0,0). El objetivo es resolver el problema de mínimos y comparar el desempeño de los algoritmos anteriores.

## Estructura del proyecto

```
Tarea-Evaluativa-Algoritmos/
├─ LICENSE                      # Licencia del repo
├─ README.md                    # Este documento
├─ code/
│  ├─ proyecto.ipynb            # Notebook principal del proyecto
│  ├─ requirements.txt          # Dependencias mínimas (jupyter, numpy, pandas, matplotlib)
│  └─ tests/                    # Salidas JSON de los experimentos (se crea al ejecutar la notebook)
│      ├─ results_YYYYMMDD_HHMMSS.json              # Experimentos masivos (puntos aleatorios)
│      ├─ param_sweep_summary_YYYYMMDD_HHMMSS.json  # Resumen del barrido de hiperparámetros
│      └─ param_sweep_detail_YYYYMMDD_HHMMSS.json   # Detalle del barrido de hiperparámetros
├─ Orden/                       # Enunciado/orden del trabajo (texto y LaTeX)
│  ├─ Orden.txt
│  └─ orden.tex
└─ Teoría/                      # Material teórico en LaTeX (marco teórico, derivadas, etc.)
	 └─ marco teorico.tex
```

### ¿Qué hay en cada carpeta?

- `code/` contiene todo lo ejecutable:
	- `proyecto.ipynb`: notebook con el flujo de trabajo, gráficos, implementación y pruebas.
	- `requirements.txt`: dependencias base del entorno.
	- `tests/`: carpeta donde se guardan los resultados de los experimentos en formato JSON con marcas de tiempo.

- `Orden/` incluye el enunciado y requisitos de la tarea (TXT/TeX).

- `Teoría/` compila el marco teórico y derivaciones (gradiente y Hessiana de la función), en LaTeX.

## Secciones de la notebook `code/proyecto.ipynb`

1. Graficación: superficie 3D y curvas de nivel con mapa de calor.
2. Algoritmos: implementación de Descenso por Gradiente y BFGS (ambos con Armijo) con docstrings y comentarios.
3. Algoritmo híbrido (GD → BFGS según radio).
4. Trayectorias: recorrido y comparación de trayectorias desde puntos iniciales concretos.
5. Experimentos masivos: lanzamientos aleatorios en [-100,100]²; los resultados se guardan en `code/tests/results_*.json`.
6. Tuning de hiperparámetros: barrido (alpha_init, beta, sigma, tol) para GD y BFGS; se generan `param_sweep_summary_*.json` y `param_sweep_detail_*.json`.
7. Conclusiones y recomendaciones.

## Cómo ejecutar

1) Instalar dependencias (opcionalmente dentro de un entorno virtual):

```
pip install -r code/requirements.txt
```

2) Abrir la notebook:

```
jupyter notebook code/proyecto.ipynb
```

3) Ejecutar las celdas en orden. Las secciones 5 y 6 generan automáticamente archivos JSON en `code/tests/` con un timestamp.

## Resultados y archivos JSON

- `results_YYYYMMDD_HHMMSS.json`: lista de corridas con campos como método, x0, iteraciones, f_final y ||∇f|| final.
- `param_sweep_summary_YYYYMMDD_HHMMSS.json`: promedios por combinación de hiperparámetros.
- `param_sweep_detail_YYYYMMDD_HHMMSS.json`: registro detallado de cada corrida del tuning.

## Hallazgos relevantes (documentados en el notebook)

- Coincidencia BFGS vs híbrido: en las ejecuciones reproducidas, las trayectorias completas generadas por BFGS y por el método híbrido coincidieron iteración a iteración (misma longitud y distancias euclideanas nulas entre iterados correspondientes).


## Contacto / Notas

- Si amplías la grilla de hiperparámetros o el número de puntos iniciales, los JSON pueden crecer rápidamente.
- La notebook incluye comentarios y fórmulas para facilitar la revisión y la defensa del proyecto.
