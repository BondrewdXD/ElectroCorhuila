# 📘 Manual de Usuario - Sistema de Gestión de Usuarios y Tarifas

## Parte Frontend - Interfaz de Usuario

---

### 🎯 Propósito del Sistema

El sistema permite a los usuarios finales gestionar su información personal y consultar las tarifas asignadas según su estrato socioeconómico. Desarrollado con **Ionic y React** para ofrecer una experiencia moderna y responsiva.

---

### 🧭 Guía de Navegación

#### Inicio

Al ingresar al sistema, se presenta una interfaz intuitiva donde el usuario puede:

- Visualizar un formulario para registrarse o actualizar sus datos  
- Consultar información relacionada con tarifas asignadas

---

### 🖥️ Pantallas del Sistema

#### 1. Formulario de Usuario

📂 **Ubicación en el proyecto:** `src/component/FormularioUsuario.tsx`

**Campos disponibles:**

- Nombre completo  
- Nombre de usuario  
- Correo electrónico  
- Contraseña  
- Estrato socioeconómico (selección)

**Funciones disponibles:**

- Ingresar y editar la información del usuario  
- Enviar datos al servidor mediante `UsuarioService`

---

### ⚙️ Funcionalidades Principales

#### ✅ Registro y edición de usuario

El formulario permite al usuario ingresar su información o actualizarla. Al enviar, se realiza una llamada al backend a través del archivo `UsuarioService.ts`.

#### 🔄 Comunicación con el backend

La lógica para la comunicación HTTP está centralizada en `UsuarioService.ts`, utilizando `fetch` o `axios` para enviar y recibir datos del servidor.
