# Matías Pérez

**Full-Stack Developer — Java, Spring Boot y Angular**<br/>
Valencia, España

Desarrollador full-stack especializado en backend con Java 21 y Spring Boot, y en frontend con Angular. Me interesa sobre todo el diseño de software que aguanta el paso del tiempo: dominios bien modelados, módulos con límites claros y tests que dan confianza para cambiar el código.

---

## Perfil

Titulado en Desarrollo de Aplicaciones Web (DAW), con un año de experiencia en producción en Inycom, donde trabajo en una aplicación del sector sanitario. Allí he pasado de corregir errores a refactorizar módulos completos, resolver incidencias críticas y participar en el análisis técnico y funcional.

En paralelo he desarrollado un sistema de gestión de restaurantes. Empezó como mi Trabajo de Fin de Grado y lo rehíce desde cero con criterios de producción: arquitectura documentada, límites entre módulos verificados en el build e integración continua en cada cambio.

En backend trabajo con arquitectura hexagonal, monolito modular, CQRS y DDD. Pongo especial cuidado en la consistencia de los datos y en la gestión de fallos con servicios externos. En frontend desarrollo con Angular moderno (Signals, OnPush, componentes standalone), con una capa HTTP bien estructurada y sin lógica de negocio en el cliente.

---

## Experiencia profesional

**Desarrollador Full-Stack · Inycom** — Valencia · Octubre 2025 – actualidad<br/>
Consultora de desarrollo de software a medida. Trabajo sobre una aplicación del sector sanitario en producción con Angular, Spring Boot y SQL Server.

**Logros**
- **Refactorización completa de uno de los cinco módulos de la aplicación, en backend y frontend, sin regresiones en producción.** Rediseñé el módulo con responsabilidades separadas, la lógica de negocio fuera de controladores y componentes, y límites claros con el resto del sistema. Consiguió **tiempos de respuesta un 60 % más rápidos** y una base preparada para escalar y mantenerse a largo plazo.
- **Código más fácil de mantener para todo el equipo.** Otros desarrolladores han destacado que corregir errores y aplicar cambios de requisito en las partes refactorizadas es ahora mucho más sencillo.
- **Desarrollo de módulos completos de extremo a extremo**, desde el análisis funcional hasta producción.
- **Resolución de incidencias críticas en producción.**
- **Referente del equipo en el dominio de negocio.** Participo en el análisis técnico y funcional, reviso requisitos con negocio y promuevo un lenguaje común entre desarrollo y cliente.

---

## Proyecto principal: sistema de gestión de restaurantes

Aplicación completa para la operativa de un restaurante. Los clientes piden y pagan desde la mesa escaneando un código QR. El personal de sala atiende en paralelo el servicio tradicional y cocina recibe las comandas en tiempo real.

Es un producto interno con código privado. Puedo enseñar el código y hacer una demostración en una entrevista.

**Funcionalidades**
- Pedidos por QR con sesión de mesa, carrito compartido entre comensales y rondas
- Pagos con Stripe, incluido el pago separado por comensal
- Pantalla de cocina y mapa de sala del camarero actualizados en tiempo real (SSE)
- Panel de administración: carta, planos de sala, personal, caja y arqueo
- Importación de la carta desde PDF mediante un modelo de lenguaje (Spring AI)
- Tickets y documentos fiscales, emails transaccionales y programa de fidelización

**Aspectos técnicos**
- Monolito modular con arquitectura hexagonal y CQRS. Los límites entre módulos se comprueban con ArchUnit en la integración continua.
- Patrón Transactional Outbox para las operaciones críticas (pagos, emails, servicios externos), con reintentos y circuit breaker mediante Resilience4j.
- Unas 2.378 clases de test en backend, con Testcontainers sobre PostgreSQL real, y unas 1000 especificaciones en frontend.
- 20 registros de decisiones de arquitectura (ADR) y documentación por módulo.

<details>
<summary><b>Detalle del backend</b></summary>

<br/>

| Área | Implementación |
|---|---|
| Arquitectura | Monolito modular con más de 17 módulos, arquitectura hexagonal, CQRS con command/query bus y eventos de dominio |
| Consistencia | Transactional Outbox (`FOR UPDATE SKIP LOCKED` y reintentos con backoff), Resilience4j (circuit breaker, retry, bulkhead), bloqueo optimista con `@Version` |
| Límites entre módulos | Tests de ArchUnit: el dominio no depende de Spring y los módulos solo se comunican a través de su API pública o de eventos |
| Persistencia | PostgreSQL con un esquema por módulo, 75 migraciones con Flyway, identificadores internos y públicos separados (`Long` / `UUID`) |
| Seguridad | Spring Security, OAuth2 y JWT, con endpoints separados por rol (administración, personal, camarero, cocina y público) |
| Rendimiento | Caché en dos niveles con Caffeine y Redis |
| Observabilidad | Actuator y Micrometer, con métricas en Prometheus y Grafana |
| Testing | JUnit 5, Testcontainers y ArchUnit |

</details>

<details>
<summary><b>Detalle del frontend</b></summary>

<br/>

| Área | Implementación |
|---|---|
| Base | Angular 17 standalone, carga diferida de rutas por área (administración, personal, cliente) y guards funcionales |
| Estado | Signals y `computed` como modelo principal; RxJS reservado para HTTP y SSE, con `toSignal` como puente; `OnPush` en todos los componentes |
| Capa HTTP | Siete interceptors: autenticación con renovación de token, gestión global de errores, idioma, indicador de carga y sesión de mesa con reintentos |
| Tiempo real | Servicios SSE sobre `EventSource` con reconexión automática |
| DOM y rendimiento | Acceso al DOM mediante `Renderer2` y `ElementRef`, `IntersectionObserver`, `@for` con `track` y sin llamadas a funciones desde las plantillas |
| Gestión de memoria | Suscripciones cerradas con `takeUntilDestroyed` |
| Seguridad | Access token en memoria y refresh token en cookie HttpOnly; frontend y API bajo el mismo origen detrás de Nginx, con cabeceras de seguridad |
| Interfaz | PrimeNG, SCSS con tokens de diseño y unidades relativas, animaciones con GSAP, gráficas con Chart.js e internacionalización con ngx-translate |
| Calidad | TypeScript estricto sin `any`, ESLint, Prettier y Stylelint |

</details>

<details>
<summary><b>Calidad, integración continua y despliegue</b></summary>

<br/>

| Área | Implementación |
|---|---|
| Entorno local | Proxy de desarrollo de Angular hacia el backend por HTTPS y Docker Compose con PostgreSQL, Redis, monitorización y SonarQube |
| Integración continua | Pipelines de GitHub Actions independientes para backend y frontend, con Checkstyle, SpotBugs, SonarQube y JaCoCo, y hook de `pre-push` |
| Documentación | ADRs, documentación por módulo y máquinas de estado de referencia |
| Despliegue | Una instalación por restaurante, réplicas sin estado y migraciones en una fase de release independiente |

</details>

La primera versión del proyecto, la del Trabajo de Fin de Grado, sigue publicada en [TFG](https://github.com/Matias048/TFG).

---

## Tecnologías

<table>
  <tr>
    <td><b>Backend</b></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/java/java-original.svg" width="36" height="36" alt="Java 21"/><br/><sub>Java 21</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/spring/spring-original.svg" width="36" height="36" alt="Spring Boot 3"/><br/><sub>Spring Boot 3</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/springsecurity/6DB33F" width="36" height="36" alt="Spring Security"/><br/><sub>Spring Security</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/spring/spring-original.svg" width="36" height="36" alt="Spring AI"/><br/><sub>Spring AI</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/hibernate/hibernate-original.svg" width="36" height="36" alt="JPA / Hibernate"/><br/><sub>JPA / Hibernate</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/gradle/gradle-original.svg" width="36" height="36" alt="Gradle"/><br/><sub>Gradle</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/stripe/635BFF" width="36" height="36" alt="Stripe"/><br/><sub>Stripe</sub></td>
  </tr>
  <tr>
    <td><b>Frontend</b></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/angular/angular-original.svg" width="36" height="36" alt="Angular"/><br/><sub>Angular</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg" width="36" height="36" alt="TypeScript"/><br/><sub>TypeScript</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/rxjs/rxjs-original.svg" width="36" height="36" alt="RxJS"/><br/><sub>RxJS</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/primeng/DD0031" width="36" height="36" alt="PrimeNG"/><br/><sub>PrimeNG</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/sass/sass-original.svg" width="36" height="36" alt="SCSS"/><br/><sub>SCSS</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/greensock/88CE02" width="36" height="36" alt="GSAP"/><br/><sub>GSAP</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/chartdotjs/FF6384" width="36" height="36" alt="Chart.js"/><br/><sub>Chart.js</sub></td>
  </tr>
  <tr>
    <td><b>Bases de datos</b></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg" width="36" height="36" alt="PostgreSQL"/><br/><sub>PostgreSQL</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/redis/redis-original.svg" width="36" height="36" alt="Redis"/><br/><sub>Redis</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/microsoftsqlserver/microsoftsqlserver-original.svg" width="36" height="36" alt="SQL Server"/><br/><sub>SQL Server</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original.svg" width="36" height="36" alt="MySQL"/><br/><sub>MySQL</sub></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/flyway/CC0200" width="36" height="36" alt="Flyway"/><br/><sub>Flyway</sub></td>
  </tr>
  <tr>
    <td><b>Testing y calidad</b></td>
    <td align="center" width="96"><img src="https://cdn.simpleicons.org/junit5/25A162" width="36" height="36" alt="JUnit 5"/><br/><sub>JUnit 5</sub></td>
    <td align="center" width="96"><img src="https://avatars.githubusercontent.com/u/13393021" width="36" height="36" alt="Testcontainers"/><br/><sub>Testcontainers</sub></td>
    <td align="center" width="96"><img src="https://raw.githubusercontent.com/TNG/ArchUnit/main/docs/assets/ArchUnit-Logo.png" width="36" height="36" alt="ArchUnit"/><br/><sub>ArchUnit</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/sonarqube/sonarqube-original.svg" width="36" height="36" alt="SonarQube"/><br/><sub>SonarQube</sub></td>
  </tr>
  <tr>
    <td><b>DevOps</b></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg" width="36" height="36" alt="Docker"/><br/><sub>Docker</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nginx/nginx-original.svg" width="36" height="36" alt="Nginx"/><br/><sub>Nginx</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/githubactions/githubactions-original.svg" width="36" height="36" alt="GitHub Actions"/><br/><sub>GitHub Actions</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/prometheus/prometheus-original.svg" width="36" height="36" alt="Prometheus"/><br/><sub>Prometheus</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/grafana/grafana-original.svg" width="36" height="36" alt="Grafana"/><br/><sub>Grafana</sub></td>
    <td align="center" width="96"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/git/git-original.svg" width="36" height="36" alt="Git"/><br/><sub>Git</sub></td>
  </tr>
</table>

---

## Otros repositorios

| Repositorio | Descripción |
|---|---|
| [TFG](https://github.com/Matias048/TFG) | Primera versión del sistema de gestión de restaurantes: Spring Boot, Angular, MySQL y Stripe |
| [patient-managment-app](https://github.com/Matias048/patient-managment-app) | Práctica de microservicios con Spring Boot |
| [Gestion-Usuarios](https://github.com/Matias048/Gestion-Usuarios) | Gestión de usuarios con API y backoffice |

---

## Idiomas

Español (nativo) · Inglés (B2)
