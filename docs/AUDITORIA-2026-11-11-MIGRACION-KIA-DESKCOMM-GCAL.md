# Auditoría y Registro de Operación: Migración KIA, Google Calendar y Desmantelamiento

**Fecha:** 2026-11-11  
**Instalación:** VPS KREO IA Studio (`2.24.72.21`) — DeskcommCRM v1.107.0  
**Organización:** KREO IA Studio (`1f467a03-052e-42e6-a4ca-3653ee632274`)  

---

## 1. Conexión de Google Calendar en DeskcommCRM
- **Estado:** `healthy`
- **Cuenta vinculada:** `kreoiastudioperu@gmail.com`
- **ID de conexión:** `116ace95-0dfd-42d8-93f0-fc6369b057b2`
- **Calendarios configurados:**
  - `kreoiastudioperu@gmail.com`: Calendario principal (`is_primary: true`, `is_destination: true`, `counts_for_conflicts: true`).
  - `Festivos en Perú`: Días no laborables (`counts_for_conflicts: false`).
- **Sincronización:** Bidireccional operativa para detección de conflictos y agendamiento de citas.

---

## 2. Configuración del Agente KIA en DeskcommCRM
- **ID de Agente:** `76cea81a-f003-4f0c-b306-b79673c51fef`
- **Modelo:** `anthropic/claude-sonnet-4-6`
- **Prompt Oficial:**
  - Identidad de Asesora Comercial y Consultora IA de KREO IA Studio.
  - Portafolio de productos: Agentes de IA WhatsApp/Web, DeskcommCRM autohospedado, Automatizaciones de flujos (SUNAT, n8n, ERPs) y Desarrollo SaaS.
  - Enlace de agendamiento directo a Google Calendar con `kreoiastudioperu@gmail.com`.

---

## 3. Chatbot Web (Landing `kreoia.site`)
- **Arquitectura nativa:** Se eliminó la dependencia del backend antiguo de FastAPI (`kreo-agente-backend`) y se migró a `kia_chat.php` en PHP-FPM dentro de `kreoia-web`.
- **Flexibilización de captura:** Apenas el visitante proporciona su WhatsApp (`+51...`) o correo electrónico, se registra de inmediato en DeskcommCRM (`crm_leads` y `contacts`) vía webhook `whk_kreoia_landing_live` y se notifica por correo a `kreoiastudioperu@gmail.com` sin esperar confirmación obligatoria.
- **Google Calendar Directo:** Erradicado `cal.com`. Ahora el botón y mensajes de agendamiento apuntan y abren directamente Google Calendar en pestaña nueva con `kreoiastudioperu@gmail.com`.

---

## 4. Desmantelamiento de Stack Antiguo (`kreoagentesdeventa`)
- **Backup de seguridad:** Guardado en `/opt/backups/kreo-agente-ventas-backup-2026-11-11.tar.gz` (80 MB).
- **Independización de Mis Finanzas:** El servicio `kreo-misfinanzas` fue aislado a `/opt/kreo-misfinanzas/` con su propio `docker-compose.yml`.
- **Contenedores eliminados:** `kreo-agente-backend`, `kreo-agente-frontend`, `kreo-agente-wa`, `kreo-agente-postgres`.
- **Almacenamiento liberado:** 114 GB libres (41% de uso en disco).

---

## 5. KREO Brain
- Registro de decisión: `02-Decisiones/ADR-2026-11-11-CONSOLIDACION-DESKCOMM-Y-DESMANTELAMIENTO-KREOAGENTESDEVENTA.md`.
- Registro de auditoría: `04-Auditorías/AUDITORIA-2026-11-11-MIGRACION-KIA-DESKCOMM-GCAL.md`.
- Memoria actualizada: `BRAIN_MEMORY.md`. Commit `0c1f29f`.
