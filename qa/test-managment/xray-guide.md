# 📘 Guía Completa de Xray y Estrategias de Pruebas

Documento profesional, visual y fácil de entender.

---

## 🧩 Índice

1. [Introducción](#-introducción)

2. [¿Qué es Xray?](#-qué-es-xray)

3. [Componentes de Xray](#-componentes-de-xray)

4. [Flujo de trabajo](#-flujo-de-trabajo-en-xray)

5. [Estrategias de pruebas](#-estrategias-de-pruebas)

6. [Pruebas de regresión](#-pruebas-de-regresión)

7. [Ejemplos prácticos](#-ejemplos-prácticos-completos)

8. [Buenas prácticas](#-buenas-prácticas)

9. [Conclusión](#-conclusión)

---

## ✨ Introducción

Xray es una herramienta de gestión de pruebas integrada a Jira que permite administrar:

- 📌 Pruebas manuales

- 🤖 Pruebas automatizadas

- 📂 Conjuntos y planes de prueba

- 🧪 Ejecuciones en diferentes entornos

- 🐞 Defectos vinculados a pruebas

- 📊 Métricas y trazabilidad

Esta guía tiene un enfoque **claro + práctico + visual** para aprender a usar Xray sin complicaciones.

---

## 🧭 ¿Qué es Xray?

Xray convierte Jira en una herramienta completa de QA con trazabilidad:

➡️ **Requerimiento → Prueba → Ejecución → Resultado → Defecto**

Sirve para:

- Organizar pruebas

- Ejecutar pruebas manuales

- Integrar pruebas automáticas

- Registrar bugs con trazabilidad

- Visualizar métricas

---

## 🧱 Componentes de Xray

### 📝 1. **Test (Caso de Prueba)**

Un test define qué se debe validar.

Puede ser:

- Manual ✋

- Automático 🤖

**Ejemplo de test manual:**

- **Objetivo:** Validar inicio de sesión exitoso.

- **Pasos:**

  1. Ingresar email válido

  2. Ingresar contraseña válida

  3. Pulsar “Login”

- **Resultado esperado:** El usuario entra al panel.

---

### 📁 2. **Test Set (Conjunto de pruebas)**

Agrupa múltiples tests relacionados.

**Ejemplo:**

**Test Set – Login (Regresión crítica)**

- Login correcto

- Login incorrecto

- Recuperar contraseña

- Validación de email

---

### 📓 3. **Test Plan (Planificación de pruebas)**

Define qué pruebas se ejecutarán en un **sprint** o **versión**.

Ideal para:

- Sprints Agile

- Regresiones

- Releases

**Estados:**

| Estado | Ícono | Definición |

|---------|-------|------------|

| Passed | ✅ | Prueba exitosa |

| Failed | ❌ | Falló la validación |

| Blocked | 🚫 | No se puede ejecutar |

| To Do | 🕒 | Pendiente |

---

### ▶️ 4. **Test Execution (Ejecución)**

Representa una corrida de pruebas.

**Ejemplo:**

**Test Execution – Sprint 7 – QA**

Incluye los tests del carrito de compras.

Una ejecución puede ser por:

- Sprint

- Entorno

- Regresión

- Release

---

### 🎯 5. **Test Run (Resultado individual)**

Un Test Run muestra:

- Estado

- Evidencias

- Fecha

- Responsable

Cada test dentro de una ejecución genera su **propio resultado**.

---

### 🐞 6. **Defects (Bugs)**

Si un test falla → se crea un **Bug vinculado automáticamente**.

Permite saber:

- Qué prueba falló

- Qué historia afecta

- Qué ejecución detectó el error

---

## 🔄 Flujo de trabajo en Xray

Flujo visual:

📌 Requerimiento (Historia de Usuario)

↓

📝 Tests creados

↓

📁 Test Set (Opcional)

↓

📓 Test Plan

↓

▶️ Test Execution

↓

🎯 Test Run (Resultado)

↓

🐞 Defectos (si los hay)

↓

📊 Reportes y Métricas

yaml

Copiar código

---

## 🧪 Estrategias de pruebas

### ✔️ Pruebas Funcionales

Validan que el sistema haga lo esperado.

Ejemplos:

- Crear usuario

- Login

- Compra

- Editar perfil

---

### ✔️ Pruebas No Funcionales

Evalúan cómo funciona el sistema.

Ejemplos:

- Velocidad ⏱️

- Seguridad 🔐

- Usabilidad 🎨

- Carga y estrés ⚡

---

### ✔️ Pruebas Exploratorias

El tester navega buscando fallos no previstos.

Ejemplos:

- Botones sin acción

- Comportamientos inesperados

- Campos mal validados

---

### ✔️ Pruebas Automatizadas

Se usan para tareas repetitivas o críticas.

Ejemplo:

- Test automático (Cypress, JUnit, etc.) ejecutado en CI/CD

- Xray recibe los resultados automáticamente

---

## 🔁 Pruebas de Regresión

Aseguran que nada que funcionaba se rompió tras un cambio.

Incluye:

- Funciones centrales

- Flujo completo

- Casos donde hubo errores en el pasado

- Validación de datos críticos

**Ejemplo real:**

Se modifica el carrito de compras.

Se prueba:

- ✔️ Agregar al carrito

- ✔️ Eliminar del carrito

- ✔️ Calcular total

- ✔️ Métodos de pago

- ✔️ Vista del carrito en el header

---

## 🧰 Ejemplos prácticos completos

### 🛒 Carrito de compras (Caso real)

**Historia de usuario:**

- `HIST-42` – Agregar producto al carrito

**Tests creados:**

- `TEST-101`: Agregar producto

- `TEST-102`: Eliminar producto

- `TEST-103`: Ver total

**Test Set:**

📁 Carrito – pruebas funcionales

**Test Plan:**

📓 Sprint 7 – Carrito

**Test Execution:**

▶️ Sprint 7 – QA – Carrito

**Resultados:**

| Test | Resultado | Notas |

|-----------|-----------|--------|

| TEST-101 | ✅ Passed | Todo ok |

| TEST-102 | ❌ Failed | Total no actualiza |

| TEST-103 | ✅ Passed | Correcto |

**Defecto creado:**

🐞 `BUG-87` – Total no actualiza al eliminar producto

---

## ⭐ Buenas prácticas

- ✔ Escribir casos de prueba claros

- ✔ Mantener Test Sets por módulos

- ✔ Crear regresiones automáticas

- ✔ Actualizar pruebas cuando cambian requerimientos

- ✔ Adjuntar evidencias (capturas o videos)

- ✔ Revisar métricas antes de liberar versiones

---

## 🏁 Conclusión

Xray es una herramienta poderosa para gestionar pruebas de manera profesional, con trazabilidad, automatización, reportes y ejecución controlada.

Con esta guía ya puedes:

- ✔ Entender cómo funciona Xray

- ✔ Crear pruebas manuales y automáticas

- ✔ Organizar pruebas por Test Sets y Test Plans

- ✔ Ejecutar y rastrear resultados

- ✔ Manejar regresiones

- ✔ Aplicar buenas prácticas

---
