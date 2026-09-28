<h1 align="center">Matías Pérez</h1>

<p align="center">
  <b>Full-Stack Developer · Java 21 · Spring Boot · Angular</b><br/>
  Construyo aplicaciones completas y mantenibles: backend con arquitectura hexagonal, CQRS y DDD, y frontend Angular reactivo con Signals.
</p>

<p align="center">
  📍 Valencia, España &nbsp;·&nbsp; 🟢 Abierto a oportunidades como Full-Stack o Backend Developer
</p>

---

## Sobre mí

Titulado en **Desarrollo de Aplicaciones Web (DAW)**. Llevo más de un año construyendo un **producto interno de gestión de restaurantes** que empezó como mi TFG y he rehecho desde cero con criterios de producción: límites entre módulos que se comprueban en el build, decisiones de arquitectura documentadas y CI que bloquea lo que no pasa.

Trabajo en las **dos capas**. En backend modelo el dominio, fijo dónde acaba cada módulo y me aseguro de que lo crítico (pagos, emails, eventos) no se pierda cuando algo falla. En frontend construyo con Angular moderno: Signals, OnPush, interceptors, tiempo real por SSE y un DOM que no se re-renderiza de más. Y siempre con cero lógica de negocio en el cliente.

Programo con **Claude Code** como herramienta del día a día, con *skills* y guías de repositorio propias que fijan las reglas de arquitectura del proyecto.

---

## Proyecto destacado: gestión de restaurantes 🍽️

> Sistema completo para un restaurante: los clientes **piden y pagan desde la mesa escaneando un QR**, el camarero atiende en paralelo el servicio tradicional y cocina recibe los tickets en tiempo real.
>
> *Producto interno con código privado. Si te interesa, te hago una demo en directo y te enseño el código.*

**Qué resuelve**
- Pedidos por QR con sesión de mesa, carrito compartido entre comensales y rondas
- Pago con **Stripe**, incluido el cobro por comensal (cada uno paga lo suyo)
- Tablero de cocina y mapa de mesas del camarero **en tiempo real por SSE**
- Panel de administración: carta, planos de sala con zonas, personal, caja y arqueo
- **Importación de la carta desde PDF con LLM** (Spring AI, Groq/Ollama detrás de un único puerto)
- Tickets y documentos fiscales (JasperReports, PDFBox), emails transaccionales y programa de puntos

**Cómo está construido: backend**

| | |
|---|---|
| **Arquitectura** | Monolito modular (17+ módulos) · hexagonal · CQRS con command/query bus · eventos de dominio |
| **Fiabilidad** | Patrón **Transactional Outbox** (`FOR UPDATE SKIP LOCKED` + reintentos con backoff) · Resilience4j (circuit breaker, retry, bulkhead) · `@Version` en agregados |
| **Límites verificados** | **ArchUnit** en CI: el dominio no importa Spring, los módulos solo se comunican por su `api/` o por eventos |
| **Datos** | PostgreSQL con esquema por módulo · 75 migraciones **Flyway** · IDs duales (`Long` interno + `UUID` público) |
| **Seguridad** | Spring Security + OAuth2 + JWT · endpoints separados por rol (admin, staff, camarero, cocina, público) |
| **Rendimiento** | Caché en dos niveles (Caffeine + Redis) |
| **Observabilidad** | Actuator + Micrometer → Prometheus + Grafana |
| **Tests** | ~290 clases de test (JUnit 5, **Testcontainers** con PostgreSQL real, ArchUnit) |

**Cómo está construido: frontend**

| | |
|---|---|
| **Base** | Angular 17 standalone · rutas con *lazy loading* por área (admin, personal, cliente) · guards funcionales |
| **Estado y reactividad** | **Signals** y `computed` como modelo por defecto · RxJS solo para flujos reales (HTTP, SSE) · `toSignal` como puente entre los dos · `OnPush` en todos los componentes |
| **Capa HTTP** | **7 interceptors** en cadena: autenticación con refresco de token, errores globales, idioma, indicador de carga y la sesión de mesa con reintentos |
| **Tiempo real** | Servicios SSE sobre `EventSource` con reconexión, que alimentan signals |
| **DOM y rendimiento** | `Renderer2` y `ElementRef` en lugar de tocar el DOM a pelo · `IntersectionObserver` · `@for` con `track` · sin llamadas a funciones en el template |
| **Memoria** | Todas las suscripciones cerradas con `takeUntilDestroyed(DestroyRef)` |
| **Seguridad** | Access token solo en memoria, refresh token en cookie HttpOnly · mismo origen detrás de Nginx, sin CORS en producción · cabeceras de seguridad en Nginx |
| **UI** | PrimeNG · SCSS con tokens de diseño y sin `px` (`rem`, `clamp()`) · animaciones con **GSAP** · gráficas con Chart.js · i18n con ngx-translate · Stripe.js |
| **Tipado y calidad** | TypeScript estricto y **cero `any`** · ESLint, Prettier y Stylelint · ~80 specs |
| **Regla de oro** | Cero lógica de negocio en el cliente: importes, repartos y arqueos los calcula el backend |

**Transversal**

| | |
|---|---|
| **Entorno local** | `proxy.conf.json` de Angular hacia el backend por HTTPS · Docker Compose con app, PostgreSQL, Redis, monitorización y Sonar |
| **Calidad y CI** | GitHub Actions separado para backend y frontend · Checkstyle · SpotBugs · SonarQube · JaCoCo · hook `pre-push` que bloquea |
| **Documentación** | **20 ADRs**, un documento por módulo y máquinas de estado canónicas |
| **Despliegue** | Una instalación por restaurante · réplicas sin estado · migraciones en un paso `release` aparte |

La primera versión, la del TFG, sigue siendo pública: **[TFG](https://github.com/Matias048/TFG)**. Comparar ese repositorio con la versión actual es la mejor forma de ver cuánto he avanzado.

---

## Stack

**Backend**
<p>
  <img src="https://img.shields.io/badge/Java_21-ED8B00?style=flat-square&logo=openjdk&logoColor=white" alt="Java 21"/>
  <img src="https://img.shields.io/badge/Spring_Boot_3-6DB33F?style=flat-square&logo=springboot&logoColor=white" alt="Spring Boot 3"/>
  <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white" alt="Spring Security"/>
  <img src="https://img.shields.io/badge/Spring_AI-6DB33F?style=flat-square&logo=spring&logoColor=white" alt="Spring AI"/>
  <img src="https://img.shields.io/badge/Hibernate_/_JPA-59666C?style=flat-square&logo=hibernate&logoColor=white" alt="Hibernate / JPA"/>
  <img src="https://img.shields.io/badge/Gradle-02303A?style=flat-square&logo=gradle&logoColor=white" alt="Gradle"/>
  <img src="https://img.shields.io/badge/Stripe-635BFF?style=flat-square&logo=stripe&logoColor=white" alt="Stripe"/>
</p>

**Datos y mensajería**
<p>
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis"/>
  <img src="https://img.shields.io/badge/Flyway-CC0200?style=flat-square&logo=flyway&logoColor=white" alt="Flyway"/>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL"/>
</p>

**Frontend**
<p>
  <img src="https://img.shields.io/badge/Angular-DD0031?style=flat-square&logo=angular&logoColor=white" alt="Angular"/>
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript"/>
  <img src="https://img.shields.io/badge/RxJS-B7178C?style=flat-square&logo=reactivex&logoColor=white" alt="RxJS"/>
  <img src="https://img.shields.io/badge/PrimeNG-DD0031?style=flat-square&logo=primeng&logoColor=white" alt="PrimeNG"/>
  <img src="https://img.shields.io/badge/SCSS-CC6699?style=flat-square&logo=sass&logoColor=white" alt="SCSS"/>
  <img src="https://img.shields.io/badge/GSAP-88CE02?style=flat-square&logo=greensock&logoColor=black" alt="GSAP"/>
  <img src="https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white" alt="Chart.js"/>
</p>

**Testing y calidad**
<p>
  <img src="https://img.shields.io/badge/JUnit_5-25A162?style=flat-square&logo=junit5&logoColor=white" alt="JUnit 5"/>
  <img src="https://img.shields.io/badge/Testcontainers-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Testcontainers"/>
  <img src="https://img.shields.io/badge/ArchUnit-555555?style=flat-square" alt="ArchUnit"/>
  <img src="https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white" alt="SonarQube"/>
</p>

**DevOps y herramientas**
<p>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker"/>
  <img src="https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white" alt="Nginx"/>
  <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions"/>
  <img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white" alt="Prometheus"/>
  <img src="https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white" alt="Grafana"/>
  <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" alt="Git"/>
  <img src="https://img.shields.io/badge/Claude_Code-D97757?style=flat-square&logo=claude&logoColor=white" alt="Claude Code"/>
</p>

---

## Otros repositorios

| Repositorio | Qué es |
|---|---|
| [TFG](https://github.com/Matias048/TFG) | Primera versión del sistema de gestión de restaurantes, mi Trabajo de Fin de Grado: Spring Boot + Angular + MySQL + Stripe |
| [patient-managment-app](https://github.com/Matias048/patient-managment-app) | Práctica de microservicios con Spring Boot |
| [Gestion-Usuarios](https://github.com/Matias048/Gestion-Usuarios) | Gestión de usuarios con API y backoffice |

---

## Qué estoy trabajando ahora

- Llevar el sistema de gestión de restaurantes a producción: una instalación por restaurante, réplicas sin estado y migraciones en un paso `release` separado
- Profundizar en sistemas distribuidos y mensajería: el siguiente paso natural después del outbox
- Mejorar mi inglés (B2 → C1)

---

## Idiomas

🇪🇸 Español, nativo &nbsp;·&nbsp; 🇬🇧 Inglés, B2

---

<p align="center">
  ¿Hablamos? Escríbeme o conéctate conmigo, y te enseño el sistema funcionando.
</p>
