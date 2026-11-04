# Extracto del contrato SLA — Agrícola Valle de Elqui SpA

## Servicio
- 2.1 Internet dedicado simétrico de 200 Mbps
- 2.2 Demarcación: Puerto LAN del CPE instalado en la planta Vicuña

## Objetivos de nivel de servicio
- 3.1 Disponibilidad ≥ 99,9 % mensual
- 3.2 Latencia: RTT promedio mensual ≤ 30 ms (ICMP cada 60 s, CPE → servidor de medición del proveedor en La Serena)
- 3.3 Jitter: Promedio mensual ≤ 10 ms (RFC 3393, TWAMP desde la demarcación)
- 3.4 Pérdida ≤ 0,5 % mensual (TWAMP desde la demarcación)
- 3.5 Throughput: Promedio de las pruebas del mes ≥ 90 % del contratado (iperf3 TCP RFC 6349 en la demarcación, mínimo 4 pruebas/mes)
- 4.1 Tiempo de respuesta ≤ 60 min desde la apertura del ticket, en el 100 % de los incidentes
- 4.2 MTTR ≤ 4 h por incidente atribuible al proveedor

## Validez y exclusiones
- 5.1 Una medición es válida solo si cubre al menos el 90 % del mes
- 6.1 Exclusiones:
  a) Mantenciones programadas avisadas con ≥ 72 h de anticipación, máximo 4 h/mes
  b) Fuerza mayor declarada
  c) Fallas atribuibles al cliente
- 6.2 Tiempo excluido se considera tiempo disponible
- 7.2 El respaldo eléctrico (UPS) del CPE es responsabilidad del cliente

## Créditos
- 8.1 Disponibilidad:
  - 99,5 % a < 99,9 % → 10 %
  - 99,0 % a < 99,5 % → 25 %
  - < 99,0 % → 50 %
- 8.2 Otros créditos: 5 % por cada incumplimiento de latencia, jitter, pérdida, throughput o tiempo de respuesta
- 8.3 Tope: 50 % del cargo mensual
- 8.4 Cargo mensual: $1.200.000 neto
