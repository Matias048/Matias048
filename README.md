<h1 align="center">Matías Pérez</h1>

<p align="center">
  <b>Backend Developer · Java 21 · Spring Boot · Angular</b><br/>
  Diseño sistemas mantenibles: monolito modular, arquitectura hexagonal, CQRS y DDD, con tests que se lo toman en serio.
</p>

<p align="center">
  📍 Valencia, España &nbsp;·&nbsp; 🟢 Abierto a oportunidades como Backend / Full-Stack Developer
</p>

---

## Sobre mí

Titulado en **Desarrollo de Aplicaciones Web (DAW)**. Llevo más de un año construyendo un **producto interno de gestión de restaurantes** que empezó como mi TFG y he rehecho desde cero con criterios de producción: límites entre módulos que se comprueban en el build, decisiones de arquitectura documentadas y CI que bloquea lo que no pasa.

Mi fuerte es el **backend**: modelar el dominio, fijar dónde acaba cada módulo y hacer que lo crítico (pagos, emails, eventos) no se pierda cuando algo falla. En frontend trabajo con Angular moderno (Signals, OnPush, standalone) y cero lógica de negocio en el cliente.

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

**Cómo está construido**

| | |
|---|---|
| **Arquitectura** | Monolito modular (17+ módulos) · hexagonal · CQRS con command/query bus · eventos de dominio |
| **Fiabilidad** | Patrón **Transactional Outbox** (`FOR UPDATE SKIP LOCKED` + reintentos con backoff) · Resilience4j (circuit breaker, retry, bulkhead) · `@Version` en agregados |
| **Límites verificados** | **ArchUnit** en CI: el dominio no importa Spring, los módulos solo se comunican por su `api/` o por eventos |
| **Datos** | PostgreSQL con esquema por módulo · 75 migraciones **Flyway** · IDs duales (`Long` interno + `UUID` público) |
| **Seguridad** | Spring Security + OAuth2 + JWT · access token en memoria, refresh token en cookie HttpOnly · endpoints separados por rol |
| **Rendimiento** | Caché en dos niveles (Caffeine + Redis) |
| **Observabilidad** | Actuator + Micrometer → Prometheus + Grafana |
| **Tests** | ~290 clases de test en backend (JUnit 5, **Testcontainers**, ArchUnit) · ~80 specs en frontend |
| **Calidad** | GitHub Actions para backend y frontend · Checkstyle · SpotBugs · SonarQube · JaCoCo · hook `pre-push` que bloquea |
| **Documentación** | **20 ADRs**, un documento por módulo y máquinas de estado canónicas |
| **Frontend** | Angular 17 standalone · Signals · OnPush · PrimeNG · ngx-translate · sin `any` y sin unidades fijas |
| **Infra** | Docker Compose (app, PostgreSQL, Redis, monitorización, Sonar) · despliegue de una instalación por restaurante |

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
