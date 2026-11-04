# Changelog

## [1.1] - 2026-11-04

### Agregado
- ejemplos/caso-valle-elqui/ con estructura completa del caso
- objetivos.yaml con umbrales, operadores, tramos de crédito y cargo mensual
- mediciones.csv con mediciones válidas del período (caídas atribuibles, latencia, jitter ponderado y throughput)
- salida_calc.txt con veredictos y cálculo de crédito
- sla.md con extracto de cláusulas del contrato
- Informe técnico de verificación de SLA (septiembre 2026)

### Cálculos manuales documentados
- Clasificación de eventos E1–E5 (atribuible / excluido)
- Promedio ponderado de jitter por número de muestras
- Verificación de tiempo de respuesta y MTTR por ticket
- Disponibilidad en serie de la infraestructura actual
- Disponibilidad con radioenlace de acceso en paralelo

### Pendiente (mejoras futuras de la calculadora)
- calc_sla.py: soporte nativo para promedio ponderado de jitter
- calc_sla.py: verificación automática de tiempo de respuesta y MTTR por ticket
- calc_sla.py: clasificación automática de eventos según cláusulas de exclusión
