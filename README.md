# Verificación de SLA — Caso Agrícola Valle de Elqui

**Asignatura:** Infraestructura de Telecomunicaciones Avanzadas  
**Carrera:** Ingeniería en Telecomunicaciones, Conectividad y Redes  
**Sede:** La Serena  
**Estudiante:** Claudio Zambra  
**Profesor:** Daniel Ruz Moreno  
**Período evaluado:** Septiembre 2026  

---

## Descripción

Informe técnico de verificación del cumplimiento del Acuerdo de Nivel de Servicio (SLA) del enlace dedicado de 200 Mbps contratado por **Agrícola Valle de Elqui SpA** a **NorteNet Telecomunicaciones**.

El objetivo es determinar, con fundamentos técnicos verificables, si el servicio cumplió las métricas pactadas durante el mes de septiembre de 2026 y calcular el crédito de servicio que corresponde.

---

## Estructura del repositorio
└── Informe_SLA_Valle_Elqui_Claudio_Zambra.pdf
├── Informe_SLA_Valle_Elqui_Claudio_Zambra.docx
├── CHANGELOG.md
├── salida_calc.txt
├── mediciones.csv
├── objetivos.yaml
├── sla.md
└── caso-valle-elqui/
└── ejemplos/
infraestructura-sla-2026/

---

## Resultado principal

| Métrica            | Objetivo     | Medido       | Veredicto              |
|--------------------|--------------|--------------|------------------------|
| Disponibilidad     | ≥ 99,9 %     | 99,63 %      | No cumple              |
| Latencia           | ≤ 30 ms      | 27,4 ms      | Cumple                 |
| Jitter             | ≤ 10 ms      | 9,74 ms      | Cumple                 |
| Pérdida            | ≤ 0,5 %      | —            | Evidencia insuficiente |
| Throughput         | ≥ 180 Mbps   | 180,75 Mbps  | Cumple                 |
| Tiempo de respuesta| ≤ 60 min     | 66 min máx.  | No cumple              |
| MTTR               | ≤ 4 h        | 75 min máx.  | Cumple                 |

**Crédito de servicio:** 15 % → **$180.000 neto**

---

## Tag de entrega

Este trabajo se entrega con el tag **v1.1**

Enlace directo: https://github.com/claudiozv/infraestructura-sla-2026/tree/v1.1
