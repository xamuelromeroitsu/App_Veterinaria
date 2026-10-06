# 🐾 VetClinic Admin & Triage — Sistema de Gestión Interna Veterinaria

**VetClinic Admin & Triage** es una solución móvil diseñada para optimizar la atención de emergencias, la gestión de consultas clínicas y el control de inventario médico en clínicas veterinarias. La aplicación facilita el flujo de trabajo operativo diario entre recepcionistas y personal médico veterinario.

---

## 📸 Capturas / Previsualización

*(Agrega aquí mockups o capturas de pantalla de la app)*

---

## 🚀 Funcionalidades Clave

### 🚑 1. Cola de Espera y Triaje dinámico
- **Clasificación por severidad:**
  - 🔴 **Rojo (Emergencia):** Atención inmediata (paro, trauma severo, hemorragia masiva).
  - 🟡 **Amarillo (Urgencia):** Atención prioritaria (fiebre alta, vomito repetido, dolor agudo).
  - 🟢 **Verde (No urgente):** Consultas de rutina, vacunación, desparasitación.
- **Gestión de estados:** Transición en tiempo real entre `Esperando`, `En Consulta` y `Alta`.

### 🩺 2. Ficha Médica e Historial Clínico
- Registro interactivo por pasos (Wizard) para evitar saturación de pantalla.
- Captura de constantes vitales con validación de rangos biológicos (Peso, Temperatura, Frecuencia Cardíaca).
- Emisión de diagnósticos y generación de recetas médicas vinculadas al inventario.

### 💉 3. Calculadora de Dosis Veterinarias Integrada
- Cálculo automático del volumen a administrar basado en la fórmula:
  $$\text{Dosis (mL)} = \frac{\text{Peso (kg)} \times \text{Concentración Dosis (mg/kg)}}{\text{Concentración Fármaco (mg/mL)}}$$
- Prevención de errores de conversión y alertas automáticas por fuera de rango.

### 📦 4. Control de Inventario & Alertas de Vencimiento
- Seguimiento de stock de medicamentos con alertas por umbral mínimo (`minThreshold`).
- Control de vencimiento por lotes de medicamentos.
- Descuento automático de existencias al prescribir en consulta.

---

## 🛠️ Arquitectura Técnica y Stack

- **Frontend Móvil:** Flutter / React Native *(selecciona tu stack)*
- **Backend as a Service:** Firebase
  - **Cloud Firestore:** Base de datos NoSQL estructurada por colecciones y subcolecciones (`triageQueue`, `patients`, `medicalRecords`, `inventory`).
  - **Firebase Authentication:** Manejo de sesiones y roles de usuario.
  - **Cloud Functions:** Disparadores para alertas automáticas de inventario y notificaciones push.
- **Validaciones:** Esquema estricto de validación en cliente y servidor para evitar inconsistencias en datos médicos.

---

## 🗄️ Esquema de Base de Datos (Cloud Firestore)

```text
/clinics/{clinicId}
├── /patients/{patientId}          --> Datos de la mascota y propietario
├── /triageQueue/{queueId}         --> Cola activa ordenada por severidad y tiempo
├── /medicalRecords/{recordId}     --> Consultas, notas y recetas médicas
└── /inventory/{itemId}            --> Lotes, stock y concentraciones de medicamentos
