# 🛣️ Diseño de Pavimentos Flexibles — Método AASHTO 93

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)
[![Licencia](https://img.shields.io/badge/Licencia-MIT-green)](LICENSE)
[![Norma](https://img.shields.io/badge/Norma-AASHTO%2093-darkblue)](https://www.transportation.org/)

> Implementación completa del procedimiento de diseño de pavimentos flexibles según la **Guía AASHTO 1993**, desarrollada como Jupyter Notebook interactivo con Python.

---

## 📋 Descripción

Este proyecto implementa el método **AASHTO 93** (*American Association of State Highway and Transportation Officials, 1993*) para el dimensionamiento estructural de pavimentos flexibles. Es la metodología más utilizada en Latinoamérica, Estados Unidos y gran parte del mundo para el diseño de carreteras nuevas y rehabilitación de pavimentos existentes.

El notebook guía al ingeniero paso a paso desde los datos de entrada hasta la obtención de los espesores de capas, pasando por todos los cálculos intermedios con sus fundamentos teóricos, fórmulas en LaTeX, tablas de referencia y visualizaciones gráficas.

---

## 🎯 Características

- ✅ **Cálculo completo de ESALs** con crecimiento geométrico del tráfico
- ✅ **Correlación CBR → Módulo Resiliente** (MR) según criterios AASHTO
- ✅ **Resolución numérica** de la ecuación AASHTO 93 (método de bisección / Brent)
- ✅ **Diseño por capas** (carpeta asfáltica, base granular, subbase granular)
- ✅ **Verificación del SN** provisto vs requerido
- ✅ **Análisis de sensibilidad** ante variaciones de MR, R, W₁₈ y ΔPSI
- ✅ **Curvas de diseño** para múltiples escenarios de confiabilidad y subrasante
- ✅ **Sección transversal** dibujada a escala con anotaciones de espesores
- ✅ **Reporte final** formateado en consola
- ✅ **Conclusiones y referencias normativas** internacionales

---

## 🗂️ Estructura del Notebook

El notebook `AASHTO93_Pavimentos_Flexibles.ipynb` está organizado en 11 secciones:

| # | Sección | Tipo | Descripción |
|---|---------|------|-------------|
| 1 | Importación de Librerías | Código | NumPy, SciPy, Matplotlib |
| 2 | Parámetros de Diseño | Markdown + Código | Datos de entrada del proyecto |
| 3 | Cálculo del Tráfico W₁₈ | Markdown + Código | ESALs acumulados con crecimiento |
| 4 | Módulo Resiliente y Z_R | Markdown + Código | MR desde CBR, confiabilidad |
| 5 | Número Estructural SN | Markdown + Código | Resolución numérica AASHTO 93 |
| 6 | Espesores de Capas | Markdown + Código | Diseño por capas D1, D2, D3 |
| 7 | Sección Transversal | Código | Visualización gráfica de la estructura |
| 8 | Análisis de Sensibilidad | Markdown + Código | Variación de parámetros clave |
| 9 | Curvas de Diseño | Código | Familias de curvas SN vs W₁₈ |
| 10 | Reporte Final | Código | Resumen tabular de resultados |
| 11 | Conclusiones | Markdown | Recomendaciones y referencias |

---

## ⚙️ Requisitos

### Python y dependencias

```
Python >= 3.8
numpy >= 1.21
scipy >= 1.7
matplotlib >= 3.4
jupyter >= 1.0
```

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/usuario/aashto93-pavimentos.git
cd aashto93-pavimentos

# Instalar dependencias
pip install -r requirements.txt

# Lanzar Jupyter
jupyter notebook AASHTO93_Pavimentos_Flexibles.ipynb
```

### `requirements.txt`

```
numpy>=1.21
scipy>=1.7
matplotlib>=3.4
jupyter>=1.0
nbformat>=5.0
```

---

## 🚀 Uso Rápido

1. **Abrir el notebook** en Jupyter Lab o Jupyter Notebook clásico.
2. **Ir a la Sección 2** — *Parámetros de Diseño*.
3. **Modificar los parámetros** del bloque de entrada según el proyecto:

```python
# --- TRÁFICO ---
ESAL_diario_inicial = 1500        # ESALs diarios en el año inicial
tasa_crecimiento    = 0.04        # Tasa de crecimiento anual (decimal)
periodo_diseno      = 20          # Período de diseño (años)
factor_direccional  = 0.50        # D_D: distribución direccional
factor_carril       = 0.90        # D_L: distribución por carril

# --- CONFIABILIDAD ---
R  = 95.0                         # Confiabilidad (%)
S0 = 0.45                         # Desviación estándar total

# --- SERVICIABILIDAD ---
pi = 4.2                          # Índice de servicio inicial
pt = 2.5                          # Índice de servicio terminal

# --- SUBRASANTE ---
CBR_subrasante = 8.0              # CBR de la subrasante (%)

# --- COEFICIENTES ESTRUCTURALES ---
a1 = 0.44    # Carpeta asfáltica
a2 = 0.14    # Base granular
a3 = 0.11    # Subbase granular
```

4. **Ejecutar todas las celdas**: `Kernel → Restart & Run All`.
5. **Leer los resultados** en la Sección 10 (Reporte Final).

---

## 📐 Fundamento Teórico

### Ecuación AASHTO 93

La ecuación de diseño es:

$$
\log(W_{18}) = Z_R \cdot S_0 + 9.36 \cdot \log(SN+1) - 0.20 + \frac{\log\!\left(\dfrac{\Delta PSI}{4.2 - 1.5}\right)}{0.40 + \dfrac{1094}{(SN+1)^{5.19}}} + 2.32 \cdot \log(M_R) - 8.07
$$

### Variables principales

| Variable | Descripción | Rango típico |
|----------|-------------|--------------|
| W₁₈ | Ejes equivalentes de 18 kips acumulados | 10⁴ – 10⁸ |
| ZR | Desviación normal estándar para confiabilidad R | −2.33 a 0.00 |
| S₀ | Desviación estándar total | 0.40 – 0.50 |
| SN | Número Estructural requerido | 1 – 12 pulg |
| ΔPSI | Pérdida de serviciabilidad (pᵢ − pₜ) | 1.5 – 3.0 |
| MR | Módulo resiliente de la subrasante | 3,000 – 30,000 psi |

### Correlación CBR → MR

```
MR (psi) = 1,500 × CBR          para CBR ≤ 10%
MR (psi) = 3,000 × CBR^0.65    para CBR > 10%
```

### Número Estructural por capas

```
SN = a₁·D₁ + a₂·m₂·D₂ + a₃·m₃·D₃
```

---

## 📊 Gráficos Generados

El notebook produce los siguientes gráficos:

| Gráfico | Descripción |
|---------|-------------|
| **ESALs acumulados** | Evolución del tráfico año a año durante el período de diseño |
| **MR vs CBR** | Curva de correlación con punto de diseño marcado |
| **Confiabilidad vs ZR** | Distribución normal para selección de ZR |
| **SN vs W₁₈** | Curva de diseño AASHTO 93 con punto de solución |
| **Sección transversal** | Estructura de capas a escala con espesores |
| **Análisis de sensibilidad** | Grilla 2×2 con variación de MR, R, W₁₈ y ΔPSI |
| **Curvas de diseño** | Familias para distintos MR y niveles de confiabilidad |

---

## 📌 Parámetros de Diseño — Guía de Referencia

### Confiabilidad recomendada por tipo de vía

| Tipo de vía | R (%) | ZR |
|-------------|-------|----|
| Caminos rurales de bajo volumen | 50 – 70 | 0.000 a −0.524 |
| Colectoras rurales | 75 – 80 | −0.674 a −0.841 |
| Arteriales rurales | 85 – 90 | −1.036 a −1.282 |
| Autopistas rurales | 90 – 95 | −1.282 a −1.645 |
| Autopistas urbanas | 95 – 99 | −1.645 a −2.327 |

### Coeficientes estructurales típicos (aᵢ)

| Material | aᵢ (pulg⁻¹) | Notas |
|----------|-------------|-------|
| Concreto asfáltico denso (CA) | 0.40 – 0.44 | Mezcla caliente, Marshall |
| CA de alta resistencia | 0.44 – 0.48 | Superpave, módulo alto |
| Base granular tipo A | 0.13 – 0.14 | CBR ≥ 80% |
| Base granular tipo B | 0.10 – 0.12 | CBR 50 – 80% |
| Subbase granular | 0.09 – 0.11 | CBR ≥ 25% |
| Subbase granular pobre | 0.07 – 0.09 | CBR 10 – 25% |

### Coeficientes de drenaje (mᵢ)

| Calidad del drenaje | Tiempo de drenaje | mᵢ |
|---------------------|-------------------|-----|
| Excelente | < 2 horas | 1.40 – 1.35 |
| Bueno | < 1 día | 1.35 – 1.25 |
| Regular | < 1 semana | 1.25 – 1.15 |
| Pobre | < 1 mes | 1.15 – 1.05 |
| Muy pobre | No drena | 1.05 – 0.95 |

---

## 🌎 Normativas de Referencia

- **AASHTO (1993).** *Guide for Design of Pavement Structures.* Washington D.C.
- **INVIAS (2013).** *Manual de Diseño Geométrico de Carreteras.* Colombia.
- **MTC (2014).** *Manual de Carreteras — Suelos, Geología, Geotecnia y Pavimentos.* Perú.
- **MTOP (2013).** *Normas de Diseño Geométrico de Carreteras.* Ecuador.
- **MOPC (2012).** *Manual de Carreteras de Paraguay.*
- **NEVI-12 (2013).** *Norma Ecuatoriana Vial.* Ecuador.


---

## ⚠️ Limitaciones y Advertencias

- El método AASHTO 93 usa **sistema inglés** internamente (psi, pulgadas, kips). Las conversiones a cm y MPa se muestran en los resultados.
- La correlación **CBR → MR** es empírica. Para proyectos importantes se recomienda determinar MR directamente con ensayo de plato de carga o ensayo triaxial de carga repetida.
- El notebook **no considera** diseño de refuerzo (overlay) ni análisis de fatiga o ahuellamiento con modelos mecanísticos.
- Los **coeficientes de drenaje mᵢ = 1.00** asumen condiciones de drenaje buenas. Ajustar si el proyecto tiene problemas de drenaje.
- Para decisiones finales de diseño, verificar con software especializado: **DARWin-ME**, **WinPAS**, **PaviCAD** o equivalente.

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Para reportar errores o sugerir mejoras:

1. Abre un *Issue* describiendo el problema o mejora.
2. Haz un *Fork* del repositorio.
3. Crea una rama con tu mejora: `git checkout -b mejora/descripcion`.
4. Envía un *Pull Request* con una descripción clara de los cambios.

---

## 📄 Licencia

Este proyecto está bajo la licencia **MIT**. Puedes usarlo, modificarlo y distribuirlo libremente con atribución al autor original.

---

## ✍️ Autor
> Autor: Mario Cesgo Soliz

> Desarrollado con Python para la comunidad de ingeniería vial hispanohablante.

> *"Un buen pavimento es invisible para el usuario; solo se nota cuando falla."*

---

*Última actualización: 2026*
