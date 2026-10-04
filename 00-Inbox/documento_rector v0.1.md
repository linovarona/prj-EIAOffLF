# Estación de Ingeniería y Automatización Offline-First (EIAOffLF)

**Estado:** Documento rector inicial
**Propósito:** Definir visión, objetivos, principios y arquitectura general del stack tecnológico
**Última actualización:** 2026-10-04

---

## 1. Propósito

Construir una estación de trabajo personal de ingeniería y automatización **offline-first**, capaz de mantener una parte sustancial del trabajo cuando la conectividad a Internet sea limitada o inexistente.

La estación no se concibe simplemente como un equipo para ejecutar modelos de lenguaje locales.

Su objetivo es proporcionar una infraestructura reutilizable para:

* desarrollo de software;
* análisis y automatización de datos;
* automatización personalizada de procesos contables y administrativos en Excel;
* documentación y gestión del conocimiento;
* investigación y documentación de procedimientos;
* automatización de procesos asociados a la creación y gestión de pequeñas y medianas empresas;
* experimentación y desarrollo de agentes;
* desarrollo del proyecto USSP de gestión/servicios de tráfico de drones.

El proyecto USSP constituye además un caso de alta complejidad que servirá para validar y hacer evolucionar la infraestructura.

---

## 2. Contexto

El trabajo profesional principal se encuentra en el análisis de datos, con una transición progresiva hacia la automatización personalizada de servicios para pequeñas y medianas empresas.

Una parte importante de estas actividades involucra:

* Excel;
* procesamiento y transformación de datos;
* procedimientos administrativos;
* documentación;
* normativa;
* formularios;
* generación de documentos;
* seguimiento de procesos;
* integración entre información y procedimientos.

**Obsidian** se utilizará como sistema central de conocimiento, planificación y documentación.

Existe además un proyecto de cliente relacionado con la implementación de una estación/sistema **USSP para tráfico de drones**. Este proyecto representa un reto técnico especialmente atractivo y servirá como campo de experimentación para arquitectura, agentes, simulación, trazabilidad, pruebas y automatización.

La conectividad a Internet es un factor limitante. Por ello, la infraestructura debe asumir desde el diseño que Internet puede no estar disponible durante períodos prolongados.

---

# 3. Principio fundamental: Offline-First

El sistema debe poder continuar funcionando en modo offline.

### En modo offline se debe poder:

* consultar el conocimiento almacenado localmente;
* trabajar en Obsidian;
* desarrollar software;
* ejecutar Python y otras herramientas locales;
* procesar archivos Excel;
* ejecutar pruebas;
* utilizar modelos de lenguaje locales;
* utilizar OpenCode;
* ejecutar agentes locales;
* trabajar con Git;
* generar documentación y artefactos;
* mantener los proyectos y su historial.

### Cuando exista conexión

La conexión debe actuar como un **acelerador**, no como una dependencia absoluta.

Se aprovechará para:

* utilizar modelos cloud de mayor capacidad;
* realizar investigación web;
* sincronizar repositorios;
* consultar fuentes externas;
* actualizar dependencias;
* descargar modelos o herramientas;
* respaldar información.

---

# 4. Principios de diseño

## 4.1 Offline-first

La ausencia de Internet no debe impedir el trabajo cotidiano.

## 4.2 Local-first para conocimiento y datos

La información de trabajo, documentación, proyectos y datos deben permanecer bajo control local.

## 4.3 Cloud como acelerador

Los modelos cloud se utilizarán cuando aporten una ventaja significativa en razonamiento, programación, investigación o revisión.

## 4.4 Human-in-the-loop

Los agentes pueden analizar, proponer, implementar y probar, pero las decisiones importantes permanecen bajo control humano.

## 4.5 Trazabilidad

Los requisitos, decisiones, código, pruebas y evidencias deben poder relacionarse entre sí.

## 4.6 Reproducibilidad

Los procedimientos importantes deben poder repetirse y quedar documentados.

## 4.7 Seguridad por defecto

Los agentes no deben disponer inicialmente de acceso indiscriminado al sistema. Las herramientas y permisos se ampliarán gradualmente.

## 4.8 Una feature a la vez

Se mantiene el principio de trabajo definido anteriormente: una única feature puede encontrarse en estado `pending` o `in_progress` a la vez.

## 4.9 Todo conocimiento importante debe quedar en archivos

Las decisiones y resultados relevantes no deben depender exclusivamente del historial de una conversación.

---

# 5. Obsidian como memoria externa de trabajo

Obsidian será el centro de conocimiento, planificación y documentación.

No se utilizará únicamente como bloc de notas.

Su función será mantener una representación estructurada del conocimiento y de los procesos.

Una estructura inicial podría ser:

```text
00-inbox/
01-vision/
02-requirements/
03-regulatory/
04-architecture/
05-domain/
06-interfaces/
07-safety/
08-security/
09-testing/
10-operations/
11-decisions/
12-research/
99-archive/
```

La estructura podrá evolucionar según las necesidades reales.

El objetivo es poder pasar de:

**conocimiento → requisito → decisión → implementación → prueba → evidencia**

---

# 6. Arquitectura general propuesta

```text
                         USUARIO
                            |
                            v
                        OBSIDIAN
                   conocimiento / plan
                            |
                            v
                       OpenCode
                     agente local
                            |
               +------------+------------+
               |                         |
               v                         v
        MODELO LOCAL                MODELO CLOUD
        Qwen3 / Ollama              programación /
        continuidad offline         razonamiento complejo
               |                         |
               +------------+------------+
                            |
                            v
                     HERRAMIENTAS
                            |
             +--------------+--------------+
             |              |              |
             v              v              v
          Python          Excel          Git
             |              |              |
             +--------------+--------------+
                            |
                            v
                    WORKER / SANDBOX
                     segunda PC
                            |
                            v
                  tests / servicios /
                  simulación / datos
```

---

# 7. Estación principal

## Hardware actual

* Intel i7-3770K
* 24 GB RAM
* SSD de 128 GB
* sin GPU dedicada
* segundo disco de 2 TB para datos

## Función

La estación principal será el centro de:

* desarrollo;
* documentación;
* Obsidian;
* OpenCode;
* modelos locales;
* integración con modelos cloud;
* Git;
* investigación;
* administración de proyectos.

## Modelo local principal

**Qwen3-8B Q4_K_M**

Se utilizará como modelo local general y como base para experimentar con agentes.

## Modelo local secundario

**Qwen3-4B cuantizado**

Se utilizará para tareas más ligeras y rápidas, clasificación, transformación, documentación y experimentación.

No se busca ejecutar simultáneamente ambos modelos como objetivo normal.

---

# 8. Segunda PC: Worker / Sandbox

## Hardware actual

* Intel i3-4150
* 8 GB RAM

## Mejora prevista

Si el coste es razonable:

* ampliar a 16 GB RAM;
* instalar SSD SATA si todavía utiliza un disco mecánico.

No se considera prioritario comprar una GPU para esta máquina.

## Función

La segunda PC no será principalmente un servidor de LLM.

Será un nodo auxiliar para:

* ejecutar scripts;
* pruebas;
* servicios locales;
* bases de datos;
* simuladores;
* contenedores;
* procesos de larga duración;
* automatizaciones;
* experimentos de agentes;
* sandbox de ejecución.

Esto permite separar:

**el lugar donde el agente razona**

de

**el lugar donde ejecuta acciones**.

---

# 9. Agentes

El objetivo no es simplemente utilizar chatbots, sino aprender y desarrollar sistemas basados en agentes.

La evolución prevista es:

```text
LLM
 |
 v
tool calling
 |
 v
agent loop
 |
 v
planificar -> ejecutar -> observar -> corregir
 |
 v
agentes especializados
 |
 v
sistemas multi-componente
```

Se explorarán herramientas como **OpenCode** y **DeepSeek Harness**.

DeepSeek Harness se considerará inicialmente un laboratorio de experimentación y aprendizaje de agentes, no un componente crítico del sistema USSP.

---

# 10. USSP como proyecto de referencia

El proyecto USSP será utilizado como caso de alta complejidad para validar la arquitectura.

Permitirá trabajar sobre:

* requisitos;
* arquitectura;
* documentación;
* trazabilidad;
* interfaces;
* simulación;
* pruebas;
* seguridad;
* automatización;
* agentes;
* revisión humana;
* gestión de cambios.

No se pretende que toda la infraestructura se diseñe exclusivamente para el USSP.

El objetivo es que el USSP ayude a desarrollar una infraestructura reutilizable para otros proyectos.

---

# 11. Automatización contable y administrativa

La misma infraestructura deberá servir para proyectos de menor escala, especialmente:

* automatización personalizada de Excel;
* análisis de datos;
* generación de documentos;
* validación de información;
* procesos administrativos;
* procedimientos contables;
* documentación de pequeñas y medianas empresas;
* ingeniería burocrática.

La idea es reutilizar la misma base:

```text
Obsidian
   |
conocimiento / procedimiento
   |
agente
   |
herramientas
   |
Python / Excel / documentos / Git
   |
resultado reproducible
```

---

# 12. Modelo de colaboración humano + IA

La distribución de responsabilidades prevista es:

### Usuario

* define objetivos;
* toma decisiones;
* valida resultados;
* aprueba cambios;
* aporta conocimiento de dominio;
* controla la dirección del proyecto.

### Modelo cloud

Actúa como apoyo de alto nivel para:

* arquitectura;
* programación compleja;
* debugging;
* revisión;
* investigación;
* diseño.

### Modelo local

Actúa como apoyo para:

* trabajo offline;
* tareas repetitivas;
* documentación;
* clasificación;
* transformación;
* navegación del proyecto;
* experimentación con agentes.

### Agente

Coordina:

* planificación;
* herramientas;
* lectura/escritura;
* ejecución;
* pruebas;
* recopilación de resultados.

---

# 13. Seguridad y control de agentes

La infraestructura debe evolucionar de forma progresiva.

Inicialmente:

```text
agente
  |
  +-- leer
  |
  +-- analizar
  |
  +-- proponer
  |
  +-- modificar workspace controlado
  |
  +-- ejecutar tests
  |
  +-- mostrar diff
  |
  v
APROBACIÓN HUMANA
```

No se permitirá inicialmente que un agente:

* modifique arbitrariamente todo el sistema;
* elimine información sin control;
* haga commits críticos automáticamente;
* despliegue sistemas de producción;
* acceda indiscriminadamente a datos personales o de clientes.

---

# 14. Git y trazabilidad

Git será el mecanismo de control de versiones.

Se mantendrá la relación:

```text
Requisito
    |
    v
Tarea
    |
    v
Implementación
    |
    v
Prueba
    |
    v
Evidencia
    |
    v
Commit
```

Cada requisito `R<n>` deberá estar asociado al menos a una prueba o, cuando se trate de un requisito diagnóstico/no ejecutable, a una evidencia apropiada.

`progress/history.md` será append-only.

---

# 15. Estrategia de hardware

No se realizará inicialmente una inversión importante en hardware.

Prioridades:

1. aprovechar el i7-3770K y sus 24 GB;
2. trasladar modelos y datos al disco de 2 TB;
3. instalar y probar Qwen3-8B Q4_K_M;
4. instalar un modelo local pequeño;
5. configurar OpenCode;
6. preparar la segunda PC como worker;
7. ampliar la segunda PC a 16 GB si resulta económico;
8. evaluar posteriormente si una GPU o actualización de plataforma produce un beneficio real.

La compra de hardware debe estar justificada por una limitación demostrada del flujo de trabajo, no por especificaciones teóricas.

---

# 16. Fases propuestas

## Fase 0 — Definición

Documentar:

* objetivos;
* arquitectura;
* principios;
* restricciones;
* criterios de éxito.

## Fase 1 — Estación offline

Preparar:

* Windows;
* disco de datos;
* estructura de directorios;
* Git;
* Python;
* Node;
* Obsidian;
* herramientas base.

## Fase 2 — LLM local

Instalar y validar:

* Ollama;
* Qwen3-8B Q4_K_M;
* Qwen3-4B;
* configuración de contexto;
* rendimiento;
* uso de RAM/CPU.

## Fase 3 — OpenCode

Configurar:

* modelo local;
* modelo cloud;
* workspace;
* permisos;
* herramientas;
* reglas de agente;
* `AGENTS.md`.

## Fase 4 — Obsidian + ingeniería

Definir:

* estructura del vault;
* plantillas;
* requisitos;
* decisiones;
* investigaciones;
* trazabilidad;
* relación con repositorios.

## Fase 5 — Worker

Preparar la segunda PC:

* RAM;
* SSD;
* sistema operativo;
* red;
* Git;
* Python;
* servicios;
* sandbox.

## Fase 6 — Primer agente

Implementar un agente controlado capaz de:

1. leer un requisito;
2. elaborar un plan;
3. pedir/aplicar aprobación;
4. modificar archivos;
5. ejecutar pruebas;
6. mostrar resultados;
7. registrar progreso.

## Fase 7 — DeepSeek Harness / laboratorio

Experimentar con:

* agent loops;
* herramientas;
* memoria;
* evaluación;
* workers;
* permisos;
* recuperación ante errores.

## Fase 8 — USSP

Aplicar la infraestructura al proyecto USSP.

## Fase 9 — Automatización empresarial

Extraer patrones reutilizables para:

* Excel;
* análisis de datos;
* contabilidad;
* documentación;
* procedimientos;
* ingeniería burocrática.

---

# 17. Criterio de éxito

La estación será considerada exitosa cuando permita realizar, sin Internet:

> **abrir un proyecto, consultar su conocimiento en Obsidian, utilizar un modelo local, desarrollar código con OpenCode, ejecutar herramientas y pruebas, documentar resultados y mantener el historial en Git.**

Cuando Internet esté disponible, el mismo entorno deberá permitir incorporar modelos cloud y fuentes externas sin cambiar fundamentalmente el flujo de trabajo.

---

# 18. Objetivo de largo plazo

Construir una **plataforma personal de ingeniería y automatización asistida por IA**, reutilizable entre distintos dominios y proyectos.

El objetivo final no es depender de un modelo concreto.

El objetivo es poseer una infraestructura donde:

```text
CONOCIMIENTO
     +
PROCEDIMIENTOS
     +
DATOS
     +
AGENTES
     +
HERRAMIENTAS
     +
MODELOS LOCALES
     +
MODELOS CLOUD
     +
CONTROL HUMANO
     =
CAPACIDAD DE AUTOMATIZACIÓN
```

La infraestructura debe permitir cambiar de modelo, herramienta o proyecto sin perder el conocimiento, los procesos, la trazabilidad ni la capacidad de trabajar offline.

---

# 19. Próximo paso

Antes de implementar componentes concretos, este documento debe convertirse en un **plan técnico ejecutable**, definiendo para cada fase:

* objetivo;
* entradas;
* salidas;
* decisiones;
* herramientas;
* configuración;
* pruebas de aceptación;
* riesgos;
* criterios para avanzar.

La implementación deberá seguir el principio:

**una fase / una feature a la vez, con validación antes de continuar.**

Este sería el documento que tomaría como **"Documento Rector v0.1"**. A partir de aquí, yo no saltaría todavía a instalar cosas: el siguiente documento debería ser el **Plan Maestro de Implementación**, donde descomponemos estas fases en tareas concretas, empezando por la Fase 0 y dejando cada fase con sus criterios de aceptación.
