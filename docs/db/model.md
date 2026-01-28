# Modelo de Datos — Wagenda (v1)

Este documento describe el **modelo de datos definitivo** del sistema **Wagenda**, una plataforma de gestión de citas para múltiples negocios, diseñada como un SaaS con una sola base de datos compartida y aislamiento lógico por negocio.

---

## 🎯 Objetivo del modelo

- Soportar múltiples negocios usando el mismo sistema
- Permitir a clientes agendar citas sin pertenecer a una sola empresa
- Mantener una arquitectura simple, escalable y profesional
- Evitar sobreingeniería en la versión inicial (v1)

---

## 🧩 Entidades principales

### 🧑 Users

Representa a todas las personas que usan el sistema.

- Incluye tanto **administradores** como **clientes**
- Los roles se gestionan mediante **Laravel Permission**
- No existe una relación directa permanente entre usuarios y negocios

**Campos:**

- id (bigint, PK)
- name (varchar)
- email (varchar, unique)
- password (varchar)
- created_at
- updated_at

---

### 🏢 Businesses

Representa a los negocios que utilizan Wagenda.

- Cada negocio pertenece a un usuario administrador (`owner_id`)
- El negocio es el eje central del dominio
- El identificador público del negocio es el `slug`

**Campos:**

- id (bigint, PK)
- owner_id (bigint, FK → users.id)
- name (varchar)
- slug (varchar, **unique**)
- description (varchar)
- created_at
- updated_at

📌 El campo `slug` se utiliza para construir la URL pública del negocio:

---

### 📅 Schedules

Define la **disponibilidad base** de un negocio.

- No representa citas
- Define reglas de horario sobre las cuales se calculan los slots disponibles

**Campos:**

- id (bigint, PK)
- business_id (bigint, FK → businesses.id)
- day_of_week (tinyint, 0 = domingo, 6 = sábado)
- start_time (time)
- end_time (time)
- slot_duration (integer, minutos)
- created_at
- updated_at

---

### 📌 Appointments

Representa una cita concreta entre un cliente y un negocio.

- Une a un usuario cliente con un negocio
- No define disponibilidad, solo ocupa un horario

**Campos:**

- id (bigint, PK)
- business_id (bigint, FK → businesses.id)
- client_id (bigint, FK → users.id)
- date (date)
- start_time (time)
- end_time (time)
- status (enum: `pending`, `confirmed`, `cancelled`)
- notes (text, nullable)
- created_at
- updated_at

---

### 🔔 Notifications

Permite mostrar notificaciones internas del sistema.

- Desacopladas de la lógica de negocio
- El contenido final se construye en el frontend usando el campo `data`

**Campos:**

- id (bigint, PK)
- user_id (bigint, FK → users.id)
- type (varchar)
- data (json)
- read_at (timestamp, nullable)
- created_at
- updated_at

---

## 🔐 Roles y permisos

Los roles y permisos se gestionan mediante el paquete **Laravel Permission**.

### Roles iniciales

- `admin`
- `client`

### Ejemplos de permisos

- manage_schedules
- view_appointments
- create_appointments
- confirm_appointments
- cancel_appointments

---

## 🔄 Reglas de negocio clave

- Un cliente **no pertenece** a un negocio; interactúa con él mediante citas
- No se puede crear una cita sin contexto de negocio (slug en la URL)
- El login identifica al usuario, **no** al negocio
- El slug identifica al negocio, **no** al usuario
- Un cliente no puede tener múltiples citas activas simultáneas en el mismo negocio
- El slug del negocio no se modifica en la versión v1
