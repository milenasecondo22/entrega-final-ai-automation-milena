# Entrega Final — Ecosistema de Automatización IA Autónomo

**Curso:** AI Automation — Coderhouse
**Alumna:** Milena Nogueira Secondo
**Caso de uso:** Clasificación automática de solicitudes de presupuesto por prioridad (Alta/Baja) para una empresa de contratistas, con validación humana (HITL) antes de contactar al cliente final.

---

## 📂 Contenido de este repositorio

| Archivo | Descripción |
|---|---|
| `Entrega-Final-Documentacion.pdf` | Documento con los 4 entregables: diagrama de arquitectura, manual de datos, matriz de costos y documentación de seguridad/resiliencia |
| `blueprint-ecosistema-final.json` | Blueprint del escenario de Make, incluyendo la lógica del HITL |
| `capturas/` | Screenshots de evidencia del flujo funcionando en Make (historial de ejecución, las 2 rutas) |

## 🔗 Enlaces obligatorios

- **Dashboard de Control (Airtable Shared View):** https://airtable.com/app869BU6q32McaEq/shrTkmzqC0oj76FLK
- **Base de datos en modo lectura:** https://airtable.com/app869BU6q32McaEq/shrTkmzqC0oj76FLK
- **Video demo:** https://drive.google.com/file/d/1VLwE-eE7zCNHiMHGRCDXo3nEDVjrVxGK/view?usp=sharing

## 🧩 Resumen del sistema

1. **Trigger:** Google Sheets detecta una fila nueva (nueva solicitud de presupuesto) en la hoja "Solicitudes".
2. **IA:** Make AI Toolkit (Categorize text) clasifica la solicitud en Prioridad Alta / Baja según M2, Inversión y Urgencia.
3. **Memoria:** El resultado se escribe en Airtable (tabla *Solicitudes*) con Estado = "Procesado por IA" y Aprobado = FALSE.
4. **Router:** Divide el flujo en 2 rutas mutuamente excluyentes (Alta / Baja), registrando cada una en Google Sheets.
5. **HITL (obligatorio):** El sistema se detiene. Un humano revisa el registro en Airtable y marca el checkbox "Aprobado".
6. **Salida multicanal:** Solo si Aprobado = TRUE, un segundo trigger dispara la respuesta al cliente por Gmail (con Thread-ID mapeado) y opcionalmente WhatsApp.
7. **Resiliencia:** Error Handler (Retry automático con 3 reintentos) sobre el nodo de IA; los fallos se registran en la tabla *Registro de Errores*.

## ✅ Criterios de evaluación cubiertos

- [x] Mapa de arquitectura (20%) — ver `Entrega-Final-Documentacion.pdf`, sección 1
- [x] Estructuras de datos documentadas (20%) — ver sección 2 (esquema Airtable + JSONs)
- [x] Optimización de costos (20%) — ver sección 3 (matriz de modelos por tarea)
- [x] Seguridad y resiliencia (20%) — ver sección 4 (minimización de datos, error handlers, HITL)
- [x] Dashboard de control (20%) — link público arriba + instrucciones de configuración en sección 5

## 🎥 Video demo

**Link:** https://drive.google.com/file/d/1VLwE-eE7zCNHiMHGRCDXo3nEDVjrVxGK/view?usp=sharing

El video muestra dos ejemplos completos de clasificación (Alta y Baja Prioridad):
1. Carga de una nueva solicitud en Google Sheets (trigger)
2. Ejecución del escenario en Make (IA clasificando en tiempo real)
3. Resultado reflejado en las hojas "Alta Prioridad" y "Baja Prioridad"
4. Vista del Dashboard de control en Airtable
