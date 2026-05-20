# Urban Traffic Dynamics: SEIR Epidemiological Modeling

## Descripción del Proyecto
Este proyecto de modelado matemático y simulación de sistemas dinámicos aborda la problemática de la congestión vehicular en la Ciudad de México desde un enfoque no convencional: aplicando el modelo epidemiológico **SEIR** (Susceptibles, Expuestos, Infectados, Recuperados). 

El objetivo es cuantificar el impacto temporal y volumétrico del tráfico en vías principales y realizar pruebas de estrés (*stress testing*) simulando distintas políticas públicas y contingencias operativas (como semáforos inteligentes, reducción del parque vehicular, construcción de vías alternas y accidentes).

**Nota:** La justificación matemática detallada y los parámetros estadísticos utilizados se encuentran en el Reporte en formato PDF adjunto en este repositorio.

## Stack Tecnológico
* **Lenguaje:** Python 3.9+
* **Cálculo Numérico y Ecuaciones Diferenciales:** SciPy (módulo `integrate.odeint`), NumPy
* **Visualización de Datos:** Matplotlib

## Metodología y Modelo Matemático
Se adaptó el modelo SEIR clásico definiendo cuatro compartimentos vehiculares:
* **S (Susceptibles):** Vehículos en tránsito normal.
* **E (Expuestos):** Vehículos disminuyendo velocidad por aproximación a zona densa.
* **I (Infectados):** Vehículos en congestión total o avance nulo.
* **R (Recuperados):** Vehículos que han abandonado el cuello de botella.

El sistema dinámico se rige por las siguientes ecuaciones diferenciales:
1. dS/dt = -β * (I/N) * S
2. dE/dt = β * (I/N) * S - σ * E
3. dI/dt = σ * E - γ * I
4. dR/dt = γ * I

*Donde:* **β** (Tasa de exposición/contagio de tráfico), **σ** (Tasa de transición al embotellamiento), y **γ** (Tasa de liberación/salida).

## Escenarios Simulados e Insights Clave
El modelo se sometió a 6 escenarios operativos partiendo de un parque vehicular simultáneo de $N = 2,240,000$ unidades:
1. **Escenario Base:** Flujo natural. El pico de congestión total alcanza 1.1 millones de vehículos al minuto 21.
2. **Semáforos Inteligentes:** Disminuyen el pico de congestión, pero prolongan la persistencia temporal del tráfico.
3. **Reducción Vehicular ("Hoy No Circula"):** Redujo la congestión máxima en un 27%, demostrando ser la variable de mayor impacto directo.
4. **Vía Alterna (Paradoja de Braess):** La infraestructura adicional retrasó el pico de congestión, pero no disminuyó el volumen total atrapado.
5. **Impulso al Transporte Público:** Redujo drásticamente el número de vehículos, pero expuso la necesidad de gestionar el flujo para evitar tiempos de recuperación alargados.
6. **Contingencia Crítica (Accidente/Clima):** Demostró la vulnerabilidad sistémica; la tasa de liberación (γ) actúa como cuello de botella irreversible, provocando un colapso que no se resuelve dentro del marco temporal simulado de 100 minutos.

## Estructura del Proyecto
* `docs/` : Reporte de investigación original (PDF).
* `simulacion_trafico_seir.ipynb` : Notebook interactivo con la implementación del modelo ODE y visualización de resultados.
* `requirements.txt` : Lista de dependencias (incluye Jupyter para ejecución).

## 🚀 Getting Started (Guía de Instalación)

Sigue estos pasos para reproducir la simulación y visualizar las curvas epidemiológicas del tráfico:

### 1. Clonar el repositorio
```bash
git clone [https://github.com/Alenkar14/urban-traffic-dynamics-seir.git](https://github.com/Alenkar14/urban-traffic-dynamics-seir.git)
cd urban-traffic-dynamics-seir
```

### 2. Configurar el entorno virtual (Recomendado)
```bash
python -m venv venv
# En Windows:
venv\Scripts\activate
# En Mac/Linux:
source venv/bin/activate
```

### 3. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 4. Ejecución de la Simulación
Ejecuta el notebook interactivo para inspeccionar el modelo y generar las gráficas dinámicas:
```bash
jupyter notebook simulacion_trafico_seir.ipynb
```
