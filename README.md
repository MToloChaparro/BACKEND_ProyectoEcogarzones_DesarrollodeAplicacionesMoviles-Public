# Ecogarzones Backend (Spring Boot + PostgreSQL)

![Kotlin](https://img.shields.io/badge/Kotlin-Android-purple?style=for-the-badge&logo=kotlin)
![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-Material_3-green?style=for-the-badge&logo=android)
![Room Database](https://img.shields.io/badge/Room-SQLite-blue?style=for-the-badge&logo=sqlite)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.3.5-brightgreen?style=for-the-badge&logo=springboot)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Supabase-336791?style=for-the-badge&logo=postgresql)

## Desarrollador
*   **Matias Toloza Chaparro**
*   **Asignatura:** Desarrollo de Aplicaciones Móviles - Sección 010D
*   **Carrera:** Ingeniería en Informática - Duoc UC sede Maipú
*   **Profesora:** Viviana Poblete

## Contexto del Negocio
Ecogarzones es una Pyme con más de seis años de trayectoria continua en el rubro de banquetería y producción de eventos sociales y corporativos en la Región Metropolitana (cumpleaños, matrimonios, cenas corporativas y activaciones de marca). La empresa ofrece una amplia oferta integral que abarca la provisión de garzones, bartenders, cocineros, coperos, animadores y supervisores de logística. Su propuesta de valor se basa en la cordialidad, la excelencia operativa y la adaptabilidad a las necesidades específicas del cliente.

## Problema y Necesidades
El modelo operativo actual presenta severos cuellos de botella e ineficiencias críticas:
*   **Tiempos de gestión elevados:** Cotizaciones por múltiples rondas de chat o llamadas, causando demoras y pérdida de clientes.
*   **Discrepancias y errores:** Omisiones respecto a restricciones alimentarias, número de invitados o insumos.
*   **Baja trazabilidad:** Falta de un panel centralizado para auditar eventos en simultáneo, horarios y control de insumos.
*   **Escalamiento complejo:** El cliente no identifica a quién dirigirse ante una incidencia en terreno.

## Objetivo del Proyecto
Digitalizar y automatizar el catálogo de servicios, permitiendo cotizaciones instantáneas y transparentes. Además, dotar al equipo en terreno y a la administración de una plataforma nativa Android, respaldada por microservicios REST, que otorgue visibilidad del flujo del servicio, control de inventario y reporte ágil de incidencias con evidencia fotográfica.

---

## Ejecutar en local
```bash
docker compose up -d db          # PostgreSQL en :5432
mvn spring-boot:run              # API en http://localhost:8080
```
Al primer arranque se cargan usuarios e inventario de prueba (ver `DataSeeder`).
Prueba rápida:
```bash
curl -X POST localhost:8080/api/usuarios/login -H "Content-Type: application/json" \
     -d '{"email":"matias@adminecogarzones.com","password":"matias123"}'
```

## Pruebas unitarias (JUnit 5 + Mockito + H2)
```bash
mvn test
```

## Deploy en la nube
**Render**: Web Service desde este repo con *Docker*. Variables de entorno:
`DB_URL` (formato JDBC, ej. `jdbc:postgresql://HOST:5432/DB?sslmode=require`), `DB_USER`, `DB_PASSWORD`.
Base de datos: Render PostgreSQL o Supabase (usa el host/puerto del *connection string*).
Render inyecta `PORT` automáticamente.

Luego en Android cambia `BASE_URL` en `RetrofitClient.kt` por `https://TU-SERVICIO.onrender.com/`.
