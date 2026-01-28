# Visión del proyecto — Wagenda

## 📌 Descripción general

Wagenda es un sistema web de gestión de citas y reservas para negocios de servicios.
Su objetivo es permitir a empresas administrar su disponibilidad y a los clientes
reservar citas de forma sencilla, ordenada y segura.

El sistema es general y no está limitado a un tipo de negocio específico
(barberías, consultorías, clínicas, asesorías, talleres, entre otros).

Está diseñado como una aplicación web moderna basada en una arquitectura
cliente-servidor, utilizando una API REST y un frontend SPA,
desplegada sobre un entorno realista con **Nginx como servidor web**.

---

## 🎯 Objetivo del proyecto

Desarrollar un proyecto personal de portafolio que demuestre:

- buenas prácticas de arquitectura backend
- correcta separación de responsabilidades
- manejo de autenticación y roles
- diseño de flujos reales de negocio
- una experiencia de usuario clara y funcional
- comprensión de un entorno de despliegue real (Nginx + API + SPA)

---

## 👥 Roles del sistema (v1)

### Administrador (Negocio)

Usuario propietario del negocio que utiliza Wagenda para gestionar sus citas.

Puede:

- configurar horarios y disponibilidad
- gestionar citas (crear, confirmar, cancelar)
- visualizar el listado de citas
- gestionar clientes
- administrar su perfil de negocio

---

### Cliente

Usuario que se registra en el sistema para agendar citas.

Puede:

- registrarse e iniciar sesión
- visualizar disponibilidad
- agendar una cita
- cancelar su cita (según reglas)
- consultar el estado de sus citas

> En la versión inicial del sistema, el cliente debe estar registrado
> para poder agendar citas.

---

## 🔄 Flujo principal del sistema

1. El negocio configura su disponibilidad
2. El cliente se registra e inicia sesión
3. El cliente visualiza los horarios disponibles
4. El cliente agenda una cita
5. El negocio confirma o cancela la cita
6. El cliente consulta el estado de su cita

Este flujo representa el núcleo funcional del sistema.

---

## 🔔 Eventos y notificaciones (planeado)

Wagenda está diseñado para emitir eventos de dominio ante acciones clave,
como la creación, confirmación o cancelación de citas.

Estos eventos permitirán:

- envío de correos electrónicos al cliente y al negocio
- notificaciones en la interfaz de usuario
- futura integración con otros canales (SMS, WhatsApp, push)
- desacoplar la lógica de negocio de los canales de comunicación

---

## 📦 Alcance inicial (v1)

- Autenticación de usuarios
- Gestión de roles
- Gestión de horarios
- Gestión de citas
- Estados de citas
- API REST
- Frontend SPA
- Despliegue mediante Nginx y PHP-FPM

---

## 🚧 Estado del proyecto

Proyecto en desarrollo, creado como iniciativa personal para portafolio profesional.
