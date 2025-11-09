# Tarea 3: Técnicas Avanzadas de Prompt Engineering

**Asignatura:** Aprendizaje de Máquinas
**Estudiante:** Francisco Encina
**Carrera:** Ingeniería Civil Telemática
**Fecha:** Noviembre 2024

---

## 📋 Descripción General

Este proyecto explora y evalúa tres técnicas avanzadas de prompt engineering: **Chain-of-Thought (CoT)**, **Tree-of-Thought (ToT)** y **Self-Refine**. El objetivo es comprender cómo estas estrategias influyen en la calidad, precisión y creatividad de las respuestas generadas por modelos de lenguaje de gran escala (LLMs).

---

## 🎯 Objetivos

1. Profundizar en técnicas de prompt engineering mediante experimentación práctica
2. Analizar cómo diferentes estrategias afectan el razonamiento de LLMs
3. Identificar fortalezas, limitaciones y casos de uso de cada técnica
4. Evaluar la confiabilidad de técnicas como Self-Refine ante errores conceptuales

---

## 🛠️ Configuración Técnica

### Modelo Utilizado
- **Modelo:** Mistral 7B Instruct v0.2
- **Plataforma:** Google Colab (GPU T4 gratuita)
- **Razón:** Balance entre rendimiento y recursos disponibles

### Dependencias
```bash
pip install transformers accelerate torch bitsandbytes
```

### Configuración
- `max_tokens`: 512 (límite intencional para análisis de comportamiento)
- `temperature`: 0.7
- `dtype`: float16

---

## 📂 Estructura del Proyecto
```
├── README.md                          # Este archivo
├── PromptEngineering.ipynb     # Notebook
```

---

## 🔬 Experimentos Realizados

### 1. Chain-of-Thought (CoT)

**Acertijos utilizados:**
- **Acertijo 1:** Tres cofres con inscripciones (solo una verdadera)
- **Acertijo 2:** Tres personas con sombreros (red/blue)

**Objetivos:**
- Comparar razonamiento con y sin Chain-of-Thought
- Evaluar si CoT mejora precisión en problemas lógicos

**Resultados clave:**
- Sin CoT: No llegó a conclusión en Acertijo 1
- Con CoT: Intentó razonar pero llegó a respuesta incorrecta (Chest B)
- Con CoT en Acertijo 2: Respuesta correcta con mejor razonamiento

**Conclusión:** CoT estructura el razonamiento pero no garantiza corrección en lógica compleja.

---

### 2. Tree-of-Thought (ToT)

**Problema:** Puzzle lógico de 5 laboratorios de IA con 15 claves interdependientes

**Variantes experimentadas:**
1. **ToT Original:** Exploración moderada con poda selectiva
2. **ToT + Verificación Lógica:** Validación exhaustiva en cada nodo
3. **ToT + Pruning Agresivo:** Poda inmediata de ramas subóptimas

**Resultados clave:**
- **ToT Original:** Exploró 3 ramas, podó correctamente, pero se truncó
- **ToT + Verificación:** Más riguroso pero consumió tokens más rápido
- **ToT + Pruning Agresivo:** FALLÓ - podó todas las ramas incluyendo la correcta

**Visualizaciones:** Dendrogramas comparativos muestran diferencias en ramificación

**Conclusión:** ToT es poderoso pero requiere calibración cuidadosa del pruning.

---

### 3. Self-Refine

**Casos experimentados:**

#### Caso 1: Infraestructura Cloud (3 data centers)
**Objetivo:** Diseñar plan de despliegue y balanceo de carga

**Proceso:**
- Iteración 0: Solución inicial
- Iteración 1-2: Refinamientos basados en auto-evaluación

**Resultado:** Mejora progresiva en completitud y detalle arquitectónico

---

#### Caso 2: Experimento de Error Intencional
**Objetivo:** Probar si Self-Refine refuerza errores conceptuales

**Setup:** Análisis de crecimiento de usuarios con sesgo intencional del "manager"

**Resultados críticos:**
- **Iteración 0:** Aceptó asunción sin verificar independientemente
- **Iteración 1:** Reforzó la asunción con "checks" tautológicos
- **Iteración 2:** Siguió reforzando, añadió "mejoras" superficiales

**Hallazgo importante:** Self-Refine NO corrigió error metodológico, sino que lo reforzó con validaciones superficiales.

**Implicación:** Self-Refine no es confiable para validar metodología, solo para refinar ejecución.

---

## 📊 Resultados Principales

### Comparativa de Técnicas

| Técnica | Mejor para | Limitación principal | Costo |
|---------|-----------|---------------------|-------|
| **CoT** | Problemas algorítmicos | Sin recuperación de errores | Bajo |
| **ToT** | Problemas complejos | Muy costoso (10-50x) | Alto |
| **Self-Refine** | Refinamiento iterativo | Refuerza errores conceptuales | Medio |

### Aplicaciones en Ing. Telemática

- **CoT:** Cálculo, física, circuitos
- **ToT:** Diseño de redes, optimización, arquitecturas
- **Self-Refine:** Documentación, ensayos, diseño de software

---

## 💡 Hallazgos Clave

1. **CoT mejora estructura pero no garantiza corrección:** Útil para transparencia, no para validación

2. **ToT con pruning agresivo es arriesgado:** Puede eliminar todas las soluciones válidas

3. **Self-Refine refuerza errores metodológicos:** Demostrado experimentalmente - solo mejora superficie, no fundamentos

4. **Limitaciones de contexto son reales:** 512 tokens fue suficiente para análisis pero insuficiente para soluciones completas

5. **La técnica debe coincidir con el problema:** No existe "mejor técnica universal"

---

## 🎓 Aprendizajes

### Teóricos
- Diferencias fundamentales entre CoT, ToT y Self-Refine
- Cómo cada técnica maneja exploración vs explotación
- Importancia de feedback externo en auto-evaluación

### Prácticos
- Implementación de LLMs en Colab con recursos limitados
- Diseño de prompts efectivos para cada técnica
- Análisis crítico de outputs de LLMs

### Críticos
- Los LLMs pueden generar respuestas coherentes pero incorrectas
- Auto-evaluación sin verificación externa es limitada
- Costo computacional es factor real en producción

---

## ⚠️ Limitaciones del Estudio

1. **Modelo único:** Solo Mistral 7B (resultados pueden variar con GPT-4, Claude, etc.)
2. **Tokens limitados:** 512 tokens truncó respuestas (intencional para análisis)
3. **Problemas específicos:** Acertijos lógicos pueden no generalizar a todos los dominios
4. **Sin métricas cuantitativas:** Análisis principalmente cualitativo
5. **Sin comparación con humanos:** No hay baseline humano de performance

---

## 📚 Referencias

### Papers Principales
1. Wei, J., et al. (2022). "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models". *NeurIPS 2022*
2. Yao, S., et al. (2023). "Tree of Thoughts: Deliberate Problem Solving with Large Language Models". *arXiv:2305.10601*
3. Madaan, A., et al. (2023). "Self-Refine: Iterative Refinement with Self-Feedback". *arXiv:2303.17651*
4. Huang, J., et al. (2023). "Large Language Models Cannot Self-Correct Reasoning Yet". *arXiv:2310.01798*

### Recursos Adicionales
- Anthropic Research: Constitutional AI and Self-Critique
- HuggingFace Transformers Documentation
- Mistral AI Official Documentation

---

## 🚀 Cómo Ejecutar

1. Abrir notebook en Google Colab
2. Configurar GPU: `Runtime > Change runtime type > GPU`
3. Ejecutar celdas en orden secuencial
4. Los experimentos generarán outputs y visualizaciones

**Nota:** Algunos experimentos pueden tardar 5-10 minutos debido a generación de múltiples iteraciones.


