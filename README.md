# 🎯 EntrevisLab

<p align="center">
  <img src="assets/banner-hero.svg" alt="EntrevisLab Banner Hero" width="100%">
</p>

<div align="center">

![EntrevisLab Version](https://img.shields.io/badge/ENTREVISLAB-v2.1%20PRODUCTION-2563EB?style=for-the-badge&logo=semanticrelease&logoColor=F8FAFC)
![Stack](https://img.shields.io/badge/STACK-VANILLA%20ES2022%20%7C%20ZERO--DEPENDENCIES-0D1526?style=for-the-badge&logo=javascript&logoColor=38BDF8)
![Security](https://img.shields.io/badge/DEVSECOPS-ZERO--XSS%20%7C%20CSP%20STRICT-10B981?style=for-the-badge&logo=cloudflare&logoColor=F8FAFC)
![Architecture](https://img.shields.io/badge/ENGINE-DETERMINISTIC%20STAR%20NLP-818CF8?style=for-the-badge&logo=githubactions&logoColor=F8FAFC)
![Privacy](https://img.shields.io/badge/PRIVACY-100%25%20CLIENT--SIDE%20EDGE-38BDF8?style=for-the-badge&logo=shieldsdotio&logoColor=060A12)

**Plataforma Web de Entrenamiento Adaptativo End-to-End para Entrevistas Técnicas y Conductuales con Motor Determinista S-T-A-R, Escáner Léxico Multi-Ofertas y Simulador por Voz en Tiempo Real.**

🌐 **[Explorar Demo Interactiva en Vivo (Cloudflare Pages)](https://entrevislab.pages.dev/)**

</div>

<p align="center">
  <img src="assets/divider.svg" alt="Separador" width="100%">
</p>

---

## 📌 1. Resumen Ejecutivo

**EntrevisLab** es un sistema de ingeniería *Frontend-Only / Zero-Backend* diseñado para resolver la asimetría entre el conocimiento técnico de un candidato y su capacidad para estructurar evidencia verbal verificable bajo presión temporal durante procesos de selección (*Screening, Assessment Grupal, Entrevista Conductual HR y Entrevista Técnica con Hiring Manager*).

> [!IMPORTANT]
> **Arquitectura de Propiedad Intelectual Protegida (Dual-Repo):** Este repositorio constituye la **Vitrina Técnica Pública (`-showcase`)** diseñada para evaluación de arquitectura, decisiones de ciberseguridad y diseño de sistemas. El código fuente propietario reside en un repositorio privado auditado con commits firmados (`Verified`).

### Indicadores Clave de Ingeniería
- **Cero Dependencias en Producción (`0 npm packages`):** Inmunidad estructural frente a ataques a la cadena de suministro (*Supply Chain Attacks*) y tiempos de carga instantáneos en el Edge.
- **Motor Léxico Determinista Bilingüe (ES/EN):** Evaluación en `< 5 ms` de estructura **S-T-A-R** (*Situación 10%, Tarea 10%, Acción 50%, Resultado 30%*), densidad de métricas contextualizadas, detección de muletillas y verbos de acción en 1.ª persona.
- **Seguridad DOM Estricta (Zero-XSS):** Prohibición total de `.innerHTML`, `.outerHTML`, `document.write()` y `eval()` verificada mediante pruebas SAST automatizadas. Todos los gráficos vectoriales se construyen en tiempo real con `document.createElementNS`.

---

## 🏗️ 2. Arquitectura del Sistema y Flujo de Datos (Paleta *Deep Navy & Metallic Silver*)

```mermaid
flowchart TB
  classDef navy fill:#0D1526,stroke:#38BDF8,stroke-width:2px,color:#F8FAFC;
  classDef primary fill:#16213A,stroke:#2563EB,stroke-width:2px,color:#F8FAFC;
  classDef action fill:#1E1B4B,stroke:#818CF8,stroke-width:2px,color:#F8FAFC;
  classDef emerald fill:#064E3B,stroke:#10B981,stroke-width:2px,color:#F8FAFC;
  classDef amber fill:#451A03,stroke:#F59E0B,stroke-width:2px,color:#F8FAFC;

  subgraph Edge["Cloudflare Edge Security & WAF"]
    CSP["Políticas HTTP (_headers)\nCSP Strict | X-Frame-Options: DENY\nPermissions-Policy: microphone=(self)"]:::amber
  end

  subgraph Presentation["Capa de Presentación y Visualización Vectorial"]
    SPA["Interfaz Semántica de 6 Fases\nTema Dual (#060A12 / #F1F5F9)"]:::navy
    SVG["Motor Gráfico SVG Seguro\ndocument.createElementNS + .textContent"]:::primary
  end

  subgraph CoreEngine["Motor Determinista Puro (ES2022 Modules)"]
    RADAR["Evaluador de 5 Ejes (0-100 pts)\nClaridad | STAR | Métricas | Tiempo | Seguridad"]:::action
    SCAN["Escáner Léxico Multi-Ofertas\nDetección de Rol, Seniority, Inglés y Niveles de Evidencia (0-3)"]:::action
    FOLLOW["Generador de Repreguntas Dinámicas\nDetección de Respuestas <20s, Divagación >150s u Omisión de KPIs"]:::action
  end

  subgraph Integrity["Integridad Criptográfica Ligera y Persistencia Local"]
    HASH["Bloqueo Secuencial Estricto\nVerificación de Evidencia con Hashes djb2"]:::emerald
    STORE[("Almacenamiento Local (localStorage)\nentrevislab_state_v2 (Schema v3)")]:::emerald
  end

  CSP --> SPA
  SPA <--> SVG
  SPA --> RADAR
  SPA --> SCAN
  SPA --> FOLLOW
  RADAR --> HASH
  SCAN --> HASH
  HASH <--> STORE
```

---

## 🔄 3. Máquina de Estados de las 6 Fases Secuenciales

<p align="center">
  <img src="assets/flow-6-fases.svg" alt="Flujo de 6 Fases" width="100%">
</p>

Cada fase exige evidencia verificable antes de desbloquear la siguiente etapa mediante cadenas de resumen criptográfico ligero (`djb2`), impidiendo la alteración manual de banderas en `localStorage`:

```mermaid
stateDiagram-v2
  classDef phase1 fill:#0D1526,stroke:#38BDF8,stroke-width:2px,color:#F8FAFC
  classDef phaseMid fill:#16213A,stroke:#2563EB,stroke-width:2px,color:#F8FAFC
  classDef phaseGym fill:#1E1B4B,stroke:#818CF8,stroke-width:2px,color:#F8FAFC
  classDef phaseFinal fill:#064E3B,stroke:#10B981,stroke-width:2px,color:#F8FAFC

  [*] --> Fase1_Diagnostico
  Fase1_Diagnostico: Fase 1 — Examen Diagnóstico (90s)\nRadar Inicial de 5 Ejes + Hash djb2
  Fase2_Escaner: Fase 2 — Gestor y Escáner Multi-Ofertas\nExtracción de Keywords, Seniority y Ruta de 4 Filtros
  Fase3_Ruta: Fase 3 — Hoja de Ruta y Micro-Learning\n5 Módulos Interactivos + Píldoras Tácticas
  Fase4_Gimnasio: Fase 4 — Gimnasio de Escenarios Guiados\nTermómetro en Vivo + Evidencia Niveles 0 a 3
  Fase5_Simulador: Fase 5 — Simulador de Entrevista Real\n4 Modos Oficiales (10 a 40 min) + Voz en Vivo
  Fase6_Dictamen: Fase 6 — Dictamen Ejecutivo\nComparativa SVG + Alineación ATS de CV + Guion .txt

  Fase1_Diagnostico --> Fase2_Escaner: diagCompletedHash válido
  Fase2_Escaner --> Fase3_Ruta: offerScannedHash válido
  Fase3_Ruta --> Fase4_Gimnasio: roadmapReviewedAt + módulo abierto
  Fase4_Gimnasio --> Fase5_Simulador: gymCompletedHash válido
  Fase5_Simulador --> Fase6_Dictamen: simCompletedHash válido
  Fase6_Dictamen --> Fase4_Gimnasio: Bucle de Afinación Continua

  class Fase1_Diagnostico phase1
  class Fase2_Escaner,Fase3_Ruta phaseMid
  class Fase4_Gimnasio,Fase5_Simulador phaseGym
  class Fase6_Dictamen phaseFinal
```

---

## 🧠 4. Ingeniería del Motor Determinista S-T-A-R y Niveles de Evidencia

<p align="center">
  <img src="assets/star-engine.svg" alt="Motor STAR y Radar" width="100%">
</p>

A diferencia de soluciones dependientes de APIs externas con latencia variable, el motor interno de **EntrevisLab** implementa algoritmos deterministas reproducibles:

| Componente Analítico | Lógica de Ingeniería Implementada | Impacto Funcional |
| :--- | :--- | :--- |
| **Normalización Léxica (`NFD`)** | Descomposición Unicode (`normalize('NFD')`) con eliminación de diacríticos y preservación de operadores porcentuales (`%`). | Garantiza paridad exacta de puntuación con o sin tildes y desde transcripciones de voz (`Web Speech API`). |
| **Clasificación de Evidencia (Niveles 0 a 3)** | Evalúa cada competencia de la oferta en cada oración: **Nivel 0** (*Ausente*), **Nivel 1** (*Mencionada*), **Nivel 2** (*Explicada con verbo de acción en 1.ª persona*), **Nivel 3** (*Demostrada con acción + métrica contextualizada*). | Evita que el candidato obtenga puntaje alto solo por listar tecnologías sin demostrar cómo las utilizó ni qué impacto logró. |
| **Filtro Anti-Falsos Positivos de Métricas** | Distingue entre años o números aislados (`bareNumbers`, ej. `"en 2024"`) e indicadores vinculados a verbos de impacto o porcentajes (`contextualMetrics`, ej. `"redujo tiempos un 35%"`). | Impide inflar artificialmente el eje de *Métricas/KPIs* en el Radar de 5 Ejes. |
| **Motor de Repreguntas Dinámicas** | Inspecciona la duración (`< 20s` o `> 150s`), la presencia de verbos en 1.ª persona (`[A]`), métricas (`[R]`) y requisitos de inglés (`B2/C1`) para sintetizar repreguntas adaptadas en tiempo real. | Entrena la capacidad de reacción del candidato ante objeciones reales de un *Hiring Manager*. |

---

## 🛡️ 5. Ciberseguridad (DevSecOps) y Pruebas Automatizadas (SAST)

<p align="center">
  <img src="assets/security-layers.svg" alt="Capas DevSecOps" width="100%">
</p>

El sistema implementa controles defensivos en profundidad verificados en cada ejecución de pruebas (`node --test`):

1. **Inmunidad contra DOM-XSS:**
   - Auditoría estática automatizada sobre los archivos de interfaz y controladores que verifica `0` ocurrencias de `.innerHTML`, `.outerHTML`, `document.write()` y `eval()`.
   - Pruebas unitarias con inyección de vectores maliciosos (`<script>alert("XSS")</script><img src=x onerror=fetch(...)>`) confirmando su neutralización total como texto plano.
2. **Protección contra Manipulación de Estado (*State Tampering*):**
   - Si un usuario intenta modificar `localStorage` para desbloquear etapas avanzadas sin evidencia real, el validador recalcula los hashes `djb2` y restablece de forma segura la etapa correspondiente.
3. **Endurecimiento en el Edge (Cloudflare Pages):**
   - Cabeceras HTTP estrictas: `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Permissions-Policy: microphone=(self), camera=(), geolocation=(), payment=()` y `Content-Security-Policy` sin orígenes de terceros no autorizados.
4. **Aislamiento en Contenedores Docker:**
   - Imagen `node:20-alpine` configurada con usuario sin privilegios (`USER node`), sistema de archivos de solo lectura (`read_only: true`) y bandera `no-new-privileges:true`.

---

## 🎨 6. Paleta Cromática Oficial (`DESIGN.md`)

| Token Visual | Código Hex | Muestra de Rol en el Sistema |
| :--- | :---: | :--- |
| **Deep Navy Canvas** | `#060A12` | Fondo principal de alto contraste ejecutivo |
| **Elevated Surface** | `#0D1526` | Paneles modulares y tarjetas de telemetría |
| **Executive Royal Blue** | `#2563EB` | Acciones primarias, navegación activa y enfoque |
| **Cyan Context `[S/T]`** | `#38BDF8` | Indicadores de Situación y Tarea (20% de la estructura) |
| **Indigo Action `[A]`** | `#818CF8` | Verbos de Acción en 1.ª Persona (50% de la estructura) |
| **Emerald Result `[R]`** | `#10B981` | Resultados cuantificados (30%), KPIs y estado óptimo |
| **Amber Alert** | `#F59E0B` | Advertencias de muletillas y presión de reloj |

---

## 👤 Autoría y Contacto Profesional

Desarrollado y arquitectado por **Lian Monsalve**.
- 🌐 **Aplicación en Vivo:** [https://entrevislab.pages.dev/](https://entrevislab.pages.dev/)
- 💼 **GitHub:** [@Lian-monsalve](https://github.com/Lian-monsalve)

**Copyright © 2026 Lian Monsalve. Todos los derechos reservados.**
