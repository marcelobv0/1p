# Predicción de aprobación en Mecánica de Materiales 1

Primer parcial del curso de Inteligencia Artificial. El notebook [parcial1_ia.ipynb](parcial1_ia.ipynb) construye un modelo de clasificación binaria que estima, **antes de que empiece el semestre**, la probabilidad de que un alumno apruebe la asignatura Mecánica de Materiales 1.

## Objetivo

Cada fila de `datos_concatenados.csv` representa el intento de un alumno en una asignatura, en un semestre y ciclo específicos. A partir de esos datos se construye una tabla donde cada fila es un intento de un alumno en Mecánica de Materiales 1, con variables conocidas al momento de la inscripción (antes de que el semestre empiece):

- Rendimiento histórico del alumno en asignaturas de semestres anteriores.
- Cuántas veces ya intentó cursar la materia objetivo.
- Datos de la inscripción actual: carrera, semestre y requisito.

La variable objetivo es `Aprobado` (`S`/`N`, convertida a `1`/`0`). El modelo, además de clasificar, entrega una probabilidad de aprobar, pensada para que alumnos y docentes puedan usarla como apoyo en acompañamiento académico.

Se usan 1.242 intentos correspondientes a los periodos 2025-1 y 2025-2 (los intentos de 2024-2 se descartan porque no cuentan con semestres previos registrados).

## Contenido del notebook

1. **Análisis de datos**: exploración del dataset completo, valores faltantes, y análisis específico de la asignatura objetivo (tasa de aprobación general, por periodo y por carrera).
2. **Procesamiento de datos**: construcción de la tabla analítica (historial académico, intentos previos, carga del semestre, dificultad relativa de materias) evitando fuga de información temporal.
3. **Entrenamiento de modelos**: Regresión Logística, Árbol de Decisión y Random Forest, todos con `class_weight="balanced"` por el desbalance de clases (16.4% aprueba).
4. **Pruebas y comparación**: métricas (Accuracy, Precision, Recall, F1, ROC-AUC, PR-AUC), validación cruzada, matrices de confusión, curvas ROC/Precision-Recall y calibración de probabilidades.
5. **Conclusiones**: Random Forest fue el modelo seleccionado (ROC-AUC de 0.943 en prueba), y las variables más asociadas con aprobar son el desempeño previo en la misma materia y el historial académico general.

## Requisitos

- Python 3.10+

## Instalación

Usando un entorno virtual:

```bash
python3 -m venv .venv
source .venv/bin/activate  # En Windows: .venv\Scripts\activate
```

Instalar las dependencias del proyecto:

```bash
pip install -r requirements.txt
```

Esto instala:

- `numpy`, `pandas` — manejo de datos
- `matplotlib`, `seaborn` — gráficos
- `scikit-learn` — modelos y métricas
- `jupyterlab`, `ipykernel` — para ejecutar el notebook

## Ejecución

Con las dependencias instaladas, abrir el notebook con JupyterLab:

```bash
jupyter lab parcial1_ia.ipynb
```

y ejecutar las celdas en orden (`Run All`). El notebook lee `datos_concatenados.csv` desde el mismo directorio, así que debe mantenerse junto al `.ipynb`.
