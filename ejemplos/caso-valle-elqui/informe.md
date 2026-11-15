# INFORME TÉCNICO DE VERIFICACIÓN DE SLA

**Caso: Agrícola Valle de Elqui SpA**  
**Período evaluado:** septiembre 2026

| Campo | Detalle |
|-------|---------|
| **NOMBRE** | Claudio Zambra |
| **CARRERA** | Ingeniería en Telecomunicaciones, Conectividad y Redes |
| **ASIGNATURA** | Infraestructura de Telecomunicaciones Avanzadas |
| **PROFESOR** | Daniel Ruz Moreno |
| **SEDE** | La Serena |
| **FECHA** | 08 de noviembre de 2026 |
| **REPOSITORIO** | https://github.com/claudiozv/infraestructura-sla-2026 · tag v1.1 |

*Evaluación Individual · Ponderación 20 % · Instrumento: escala de apreciación*  
*A. Esperado: 1.1.4 · 1.1.5*

---

## 01. Identificación

| Campo | Detalle |
|-------|---------|
| Servicio | Internet dedicado simétrico 200 Mbps (Cláusula 2.1) |
| Cliente / Proveedor | Agrícola Valle de Elqui SpA / NorteNet Telecomunicaciones |
| Período evaluado | 01 al 30 de septiembre de 2026 · 30 días · 43.200 min |
| Punto de demarcación | Puerto LAN del CPE instalado en la planta Vicuña (Cláusula 2.2) |
| Cargo mensual neto | $1.200.000 CLP (Cláusula 8.4) |
| Integrante | Claudio Zambra |
| Repositorio | https://github.com/claudiozv/infraestructura-sla-2026 · tag v1.1 |

---

## 02. Resumen ejecutivo

Durante el período de septiembre de 2026 el servicio no cumple el SLA. Incumple disponibilidad (99,63 % frente a ≥ 99,9 %) y tiempo de respuesta (66 min frente a ≤ 60 min). Cumplen latencia, jitter, throughput y MTTR. La métrica de pérdida presenta evidencia insuficiente (cobertura < 90 %). Corresponde un crédito de servicio del 15 % (10 % por disponibilidad + 5 % por tiempo de respuesta), equivalente a $180.000 CLP netos.

---

## 03. Alcance y referencias

Se evalúan las cláusulas 3.1 (Disponibilidad), 3.2 (Latencia), 3.3 (Jitter), 3.4 (Pérdida), 3.5 (Throughput), 4.1 (Tiempo de respuesta) y 4.2 (MTTR). Cláusulas regulatorias: 5.1 (Validez de la medición), 6.1 y 6.2 (Exclusiones), 7.2 (Respaldo energético) y 8.1 a 8.4 (Créditos y topes). Normas de medición aplicadas: ITU-T Y.1540/Y.1541, RFC 3393, RFC 5357 (TWAMP), RFC 6349 (iperf3) e ITU-T E.860.

---

## 04. Metodología — Variables y validez de la evidencia

### Tabla de variables por métrica

| Métrica | Operador / umbral | Estadístico | Fuente válida | Cobertura | Fuente descartada |
|---------|-------------------|-------------|---------------|-----------|-------------------|
| Disponibilidad | ≥ 99,9 % | Mensual | NMS + tickets | 100 % | — |
| Latencia | ≤ 30 ms | Promedio | Zabbix cliente | 98,9 % | Proveedor (PE–core) |
| Jitter | ≤ 10 ms | Promedio | TWAMP cliente | 98,9 % | — |
| Pérdida | ≤ 0,5 % | Mensual | — | < 90 % | TWAMP incompleto / PE–core |
| Throughput | ≥ 180 Mbps | Promedio | iperf3 en CPE (4) | 4 de 4 | Speedtest Wi-Fi |
| Respuesta | ≤ 60 min | 100 % tickets | Tickets | 3 de 3 | — |
| MTTR | ≤ 4 h | Por incidente | NMS + tickets | — | — |

### Evaluación de evidencias

- **Latencia Zabbix cliente:** Aceptada. Cobertura 42.725 / 43.200 = 98,90 % ≥ 90 % (Cláusula 5.1). Las 475 muestras faltantes coinciden con los períodos de caída.
- **Reporte de latencia del proveedor:** Descartado. Medido entre PE y Core en Santiago, fuera del punto de demarcación (Cláusula 2.2).
- **Throughput iperf3 (CPE LAN):** Aceptado. 4 pruebas en el puerto LAN del CPE bajo RFC 6349.
- **Speedtest web gerencia (95 Mbps):** Descartado. Realizado desde notebook por Wi-Fi, sin validez técnica ni cumplimiento de demarcación.
- **Pérdida TWAMP:** Evidencia insuficiente. Colector detenido el 19-sep por disco lleno → cobertura < 90 %.

### Información faltante

Falta la serie completa de muestras TWAMP de pérdida para el período 19-30 de septiembre. Sin ella no es posible emitir veredicto de cumplimiento sobre la métrica de pérdida de paquetes.

---

## 05. Resultados de evaluación

### a) Clasificación de eventos de caída

| Ev. | Fecha / Horario | Duración | Clasificación | Fundamento y cláusula |
|-----|-----------------|----------|---------------|-----------------------|
| E1 | 03-sep 02:00–05:30 | 210 min | Excluido | Mantenimiento programado. Aviso 29-ago (112 h ≥ 72 h); 3,5 h ≤ 4 h/mes (Cláusula 6.1a) |
| E2 | 09-sep 14:12–15:07 | 55 min | Atribuible | Corte de fibra por obras viales (INC-2611). Responsabilidad del acceso del proveedor |
| E3 | 15-sep 10:40–12:25 | 105 min | Excluido | Corte eléctrico en planta cliente (INC-2648). CPE sin UPS (Cláusulas 6.1c y 7.2) |
| E4 | 21-sep 22:05–23:20 | 75 min | Atribuible | Falla de tarjeta de línea en PE La Serena (INC-2672). Hardware del proveedor |
| E5 | 27-sep 08:30–09:00 | 30 min | Atribuible | Mantención de emergencia (INC-2690). Aviso 26-sep 18:00 (14,5 h < 72 h) |

**Caída atribuible total = 55 + 75 + 30 = 160 min.**

### b) Cálculos matemáticos justificados

**1. Disponibilidad mensual**
T_total = 30 × 24 × 60 = 43.200 min
T_caída atribuible = E2 (55) + E4 (75) + E5 (30) = 160 min
Disponibilidad = (43.200 − 160) / 43.200 × 100 = 99,6296 % ≈ 99,63 %
Caída permitida (99,9 %) = 43.200 × 0,001 = 43,20 min
Exceso de caída = 160 − 43,20 = 116,80 min → NO CUMPLE (crédito 10 %)

Texto

**2. Jitter mensual ponderado por muestras**
Muestras totales = 9.870 + 10.025 + 9.900 + 12.930 = 42.725
Suma ponderada = (9,0×9.870) + (10,5×10.025) + (13,8×9.900) + (7,2×12.930) = 415.942,5
Jitter promedio = 415.942,5 / 42.725 = 9,74 ms ≤ 10,0 ms → CUMPLE

Texto

**3. Throughput promedio (iperf3 TCP)**
Throughput = (186 + 182 + 171 + 184) / 4 = 723 / 4 = 180,75 Mbps
Umbral contractual = 200 × 0,90 = 180 Mbps → 180,75 ≥ 180 → CUMPLE

Texto

**Latencia:** Promedio mensual medido 27,4 ms ≤ 30 ms → **CUMPLE**. El contrato fija el promedio mensual como estadístico de evaluación.

**Pérdida:** Evidencia insuficiente (cobertura < 90 %).

### c) Tiempo de respuesta y MTTR

| Ticket | Respuesta | ≤ 60 min | Restauración | ≤ 4 h | Origen |
|--------|-----------|----------|--------------|-------|--------|
| INC-2611 | 23 min | Sí | 55 min | Sí | Proveedor |
| INC-2648 | 33 min | Sí | No aplica | — | Cliente |
| INC-2672 | 66 min | No | 75 min | Sí | Proveedor |
| INC-2690 | 7 min | Sí | 30 min | Sí | Proveedor |

Tiempo de respuesta: no se cumple en el 100 % de los incidentes atribuibles (INC-2672 = 66 min > 60 min). MTTR: se cumple en todos los incidentes atribuibles.

### d) Matriz general de resultados

| Métrica | Objetivo | Medido | Desviación | Fuente | Veredicto | Crédito |
|---------|----------|--------|------------|--------|-----------|---------|
| Disponibilidad | ≥ 99,9 % | 99,63 % | −0,27 pp | NMS + tickets | NO CUMPLE | 10 % |
| Latencia | ≤ 30 ms | 27,4 ms | — | Zabbix cliente | CUMPLE | — |
| Jitter | ≤ 10 ms | 9,74 ms | — | TWAMP cliente | CUMPLE | — |
| Pérdida | ≤ 0,5 % | — | — | TWAMP incompleto | Evid. insuf. | — |
| Throughput | ≥ 180 Mbps | 180,75 Mbps | +0,75 Mbps | iperf3 CPE | CUMPLE | — |
| T. Respuesta | ≤ 60 min | 66 min máx. | +6 min | Tickets | NO CUMPLE | 5 % |
| MTTR | ≤ 4 h | 75 min máx. | — | NMS + tickets | CUMPLE | — |

---

## 06. Análisis de incumplimientos

| Incumplimiento | Cuándo | Causa | Impacto en el negocio | Origen |
|----------------|--------|-------|-----------------------|--------|
| Disponibilidad | 09, 21 y 27-sep | Corte de fibra por obras viales; falla de tarjeta de línea en PE; mantención de emergencia sin aviso suficiente | 160 min sin ERP, trazabilidad de exportación ni telefonía IP | Proveedor |
| Tiempo de respuesta | 21-sep (INC-2672) | Primera respuesta a las 66 min desde la apertura del ticket | Retraso en el inicio del diagnóstico de la falla de tarjeta de línea | Proveedor |

---

## 07. Conclusiones técnicas

### Veredicto global

El servicio no cumple el SLA de septiembre de 2026. Se verificaron incumplimientos en disponibilidad y tiempo de respuesta. Latencia, jitter, throughput y MTTR cumplen. La métrica de pérdida no puede evaluarse por evidencia insuficiente.

### Liquidación de créditos de servicio

| Concepto | Valor |
|----------|-------|
| Crédito por disponibilidad (Cláusula 8.1) — tramo 99,5 % a < 99,9 % | 10 % ($120.000) |
| Crédito por tiempo de respuesta (Cláusula 8.2) | 5 % ($60.000) |
| Crédito total | 15 % |
| Tope contractual | 50 % |
| Crédito aplicable | 15 % (≤ tope) |
| Monto (cargo $1.200.000) | **$180.000 neto** |

### Viabilidad del objetivo de disponibilidad 99,9 %
Modelo serie (actual): Aserie = 0,9995 × 0,9980 × 0,9999 × 0,9999 = 99,73 %
99,73 % < 99,9 % → el objetivo no es viable con ruta única de fibra.

Modelo paralelo (radioenlace 99,50 %): Aacceso = 1 − (1−0,9980)×(1−0,9950) = 99,999 %
Anueva ≈ 99,94 % ≥ 99,9 % → con respaldo en paralelo el objetivo se vuelve viable.

Texto

### Respuesta al gerente de operaciones

| Afirmación del gerente | ¿Se sostiene? | Fundamento |
|------------------------|---------------|------------|
| “Septiembre fue un desastre. Se cayó varias veces” | Parcialmente | Hubo 5 eventos. Solo 3 son atribuibles al proveedor (160 min). Dos están excluidos por contrato. |
| Speedtest 95 Mbps cuando se pagan 200 Mbps | No | Herramienta, punto y medio (Wi-Fi) no pactados. El promedio iperf3 en demarcación es 180,75 Mbps y cumple. |
| Peaks de 118 ms en Zabbix | No como incumplimiento | El contrato evalúa el promedio mensual (27,4 ms ≤ 30 ms). El máximo no es el estadístico pactado. |
| Exigir el crédito máximo (50 %) | No | El crédito calculado es 15 % ($180.000). El tramo de 50 % solo aplica si la disponibilidad es < 99,0 %. |

---

## 08. Recomendaciones

| Hallazgo | Recomendación técnica | Qué mejora | Prioridad |
|----------|-----------------------|------------|-----------|
| Fibra de acceso única limita disponibilidad a 99,73 % | Contratar el radioenlace de acceso ofrecido como respaldo con ruta diversa | Eleva la disponibilidad teórica a ≈ 99,94 %, haciendo viable el SLA de 99,9 % | Alta |
| Tiempo de respuesta 66 min en INC-2672 | Solicitar al proveedor el registro de tiempos de respuesta y un plan de mejora del NOC | Cumplimiento de la cláusula 4.1 | Alta |
| CPE sin respaldo eléctrico (105 min caída E3) | Instalar UPS dedicada de al menos 1 kVA en el rack del CPE | Evita caídas del servicio ante cortes de energía en la planta | Alta |
| Colector TWAMP detenido por disco lleno | Implementar monitoreo de espacio en disco y alertas proactivas del colector | Cobertura de evidencia de pérdida y jitter | Media |
| Mediciones informales (Speedtest) | Definir protocolo interno de pruebas solo con iperf3 en el puerto LAN del CPE | Evidencia válida para reclamaciones | Baja |

---

## 09. Automatización del proceso

### Flujo de generación del informe

| Paso | Entrada | Proceso | Salida |
|------|---------|---------|--------|
| 1 | Anexos del caso | Carga manual de datos | objetivos.yaml y mediciones.csv |
| 2 | YAML + CSV | calc_sla.py | salida_calc.txt con veredictos y crédito |
| 3 | Salida + plantilla | Redacción / generación | informe.md |
| 4 | informe.md | pandoc u otra conversión | informe.pdf |
| 5 | Carpeta del caso | Commit, merge y tag | Versión v1.1 publicada |

**Pasos automatizados:** ejecución de calc_sla.py y conversión a PDF.  
**Pasos manuales:** clasificación de eventos, cálculo del jitter ponderado, verificación de tiempos de respuesta/MTTR, análisis de viabilidad serie/paralelo y redacción de recomendaciones.

### Comandos para regenerar el informe

```bash
python3 herramientas/calc_sla.py \
  -o ejemplos/caso-valle-elqui/objetivos.yaml \
  -m ejemplos/caso-valle-elqui/mediciones.csv \
  > ejemplos/caso-valle-elqui/salida_calc.txt

pandoc ejemplos/caso-valle-elqui/informe.md \
  -o ejemplos/caso-valle-elqui/informe.pdf
Anexos
A. objetivos.yaml (extracto)
YAML
servicio: "Internet dedicado 200 Mbps - Agricola Valle de Elqui"
periodo: "2026-09"
minutos_periodo: 43200
cobertura_minima: 0.90
cargo_mensual: 1200000
tope_credito: 0.50
metricas:
  disponibilidad: {operador: ">=", objetivo: 99.9, unidad: "%"}
  latencia: {operador: "<=", objetivo: 30, unidad: "ms", estadistico: promedio}
  jitter: {operador: "<=", objetivo: 10, unidad: "ms", estadistico: promedio}
  perdida: {operador: "<=", objetivo: 0.5, unidad: "%"}
  throughput: {operador: ">=", objetivo: 180, unidad: "Mbps", estadistico: promedio}
creditos_disponibilidad:
  - {desde: 99.5, hasta: 99.9, credito: 0.10}
  - {desde: 99.0, hasta: 99.5, credito: 0.25}
  - {desde: 0.0,  hasta: 99.0, credito: 0.50}
credito_otras: 0.05
B. mediciones.csv (mediciones válidas)
Csv
fecha,metrica,valor,unidad
2026-09-09,caida_atribuible,55,min
2026-09-21,caida_atribuible,75,min
2026-09-27,caida_atribuible,30,min
2026-09-30,latencia,27.4,ms
2026-09-30,jitter,9.74,ms
2026-09-05,throughput,186,Mbps
2026-09-12,throughput,182,Mbps
2026-09-19,throughput,171,Mbps
2026-09-26,throughput,184,Mbps
C. Cálculos manuales no cubiertos por la calculadora
Clasificación de eventos E1–E5 con citación de cláusulas.
Promedio ponderado de jitter por número de muestras.
Verificación de tiempo de respuesta y MTTR por ticket.
Cálculo de disponibilidad en serie y con respaldo en paralelo.
Evaluación de cobertura de la métrica de pérdida.
D. Versionado
Bash
git tag -a v1.1 -m "v1.1: caso Agrícola Valle de Elqui"
git push origin main --tags
Enlace del repositorio: [github.com/claudiozv/infraestructura-sla-2026](https://github.com/claudiozv/infraestructura-sla-2026)
Tag de entrega: v1.1
