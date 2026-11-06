# Artículo científico AgriSmart — tema (5-nov-2026, actualizado 6-nov-2026)

**Título (es):** Evaluación experimental de arquitecturas cloud-céntrica, fog on-premise e híbrida edge–fog–cloud para la delimitación de zonas de manejo agrícola mediante clustering con restricciones de tamaño: caso AgriSmart, Latacunga, Ecuador

**Title (en):** Experimental Evaluation of Cloud-Centric, On-Premise Fog and Hybrid Edge–Fog–Cloud Architectures for Size-Constrained Clustering of Agricultural Management Zones: The AgriSmart Case in Latacunga, Ecuador

**Objetivo:** Evaluar experimentalmente tres arquitecturas de despliegue (cloud-céntrica, fog on-premise e híbrida edge–fog–cloud) para la delimitación de zonas de manejo agrícola mediante clustering con restricciones de tamaño sobre datos de suelo, en términos de tiempo de respuesta, throughput, consumo de recursos, tolerancia a desconexiones, costo por trabajo y calidad de las zonas generadas.

**Datos:** SoilGrids 2.0 (ISRIC, 250 m) para la parroquia 11 de Noviembre; NPK sintético calibrado con rangos del INIAP; validación con 4 nodos ESP32 LoRa en visitas de campo (no instalados de forma permanente).

**Enfoque propio (no es el tema docente 11 de Diego Vallejo):** se comparan ubicaciones de despliegue (cloud / fog en servidores HP / híbrido), no estilos monolito–colas–microservicios.

**Autoría:** 2 autores; Manuel Villa primer autor y de correspondencia. 40 estudiantes (8 grupos de 5) en agradecimientos. Financiamiento: proyecto de investigación formativa AgriSmart Latacunga (UTC). En el artículo se menciona el proyecto en introducción, métodos (desarrolla su objetivo específico 1), financiamiento y agradecimientos, sin copiar su texto.

**Horas de los estudiantes:** 240 h por estudiante, contadas desde el lunes 9-nov-2026 e incluidas las semanas del anteproyecto: 10 h/sem en S1–S4 (40), 12 en S5–S6 (24), 16 en S7–S15 (144), 8 en S16–S19 (32). Registro semanal en la hoja de horas que lleva G8.

**Materiales:** ya disponibles placas ESP32 LoRa y power banks. Compra para el artículo: 6 sensores capacitivos de humedad de suelo, 5 DS18B20, 5 SHT31 (53–95 USD) + AWS (30–80 USD). Nodos de campo permanentes y sensor 7 en 1 (pH/NPK) después, para el proyecto. Archivo: `Lista_materiales_AgriSmart.xlsx`.

**Fila 15 de la hoja de propuestas:** tema, objetivo y alcance redactados en el formato de los docentes (archivo `Propuesta_Docentes_con_tema_AgriSmart.ods`).

## Repositorio base para los estudiantes (6-nov-2026)
Archivo `agrismart-arquitecturas.zip` (en D:\26-26\MAESTRIA). Contiene:
- `service/`: servicio común FastAPI (k-means, k-means con restricciones de tamaño vía algoritmo húngaro, MILP p-mediana capacitada con PuLP), métricas de calidad, Prometheus; 7 pruebas pasan.
- `deploy/cloud`, `deploy/fog`, `deploy/hybrid`: docker-compose por arquitectura (PostGIS, Mosquitto, ingesta MQTT, sincronizador outbox fog→nube), monitoreo con Prometheus/Grafana.
- `edge/`: firmware ESP32 (Heltec V3 / LilyGO T3) con store-and-forward y ACK, gateway LoRa→MQTT, simulador de nodos.
- `data/`: SoilGrids, NPK sintético, carga a PostGIS, solicitudes; `experiments/`: 810 corridas de rendimiento y 60 de resiliencia en orden aleatorio, k6, inyección de fallos; `analysis/`: ANOVA/Kruskal-Wallis con Holm y figuras.
- `docs/`: arquitecturas, contrato de API, guía por grupo, experimentos, 3 ADR.
Pendiente de verificar en campo: levantar los compose en AWS y en el servidor HP, sincronizador con PostgreSQL real, descarga de SoilGrids, compilar el firmware.

## Cronograma (página: https://claude.ai/artifact/Qi7UkmhvRRkZvkRJj4EtFi)
Primero se aprueba el anteproyecto (aprobación esperada el jueves 3-dic-2026); el artículo se ejecuta después. Los estudiantes adelantan la parte técnica en paralelo desde el 9-nov como actividades del proyecto AgriSmart. Sin pausa de fin de año (decisión del 6-nov): solo feriados 25 dic y 1 ene.
- Fase 0 Anteproyecto: S1–S4 (9 nov–4 dic) · entrega 27 nov · H1 aprobación (S4)
- Fase 1 Arranque y literatura: S5–S8
- Fase 2 Datos (SoilGrids, NPK, nodos ESP32): S6–S10
- Fase 3 Algoritmos MILP + k-means y API OpenAPI: S7–S10 · H2 (S10: 11–15 ene)
- Fase 4 Arquitecturas cloud, fog, híbrida, CI/CD, C4/ADR: S10–S13 · H3 (S13: 1–5 feb)
- Fase 5 Experimentos (30 repeticiones, fallos de red, visitas de campo): S13–S15 · H4 (S15: 15–19 feb)
- Fase 6 Análisis, redacción, revisión, Turnitin y envío: S16–S19 · H5 (S18: 8–12 mar), H6 envío (S19: 15–19 mar 2027)
Feriados: 25 dic, 1 ene, Carnaval 8–9 feb. Depósito de titulación UPS: mayo 2027.
Grupos: G1 datos y SIG · G2 algoritmos · G3 nube · G4 fog · G5 edge e IoT · G6 pruebas y observabilidad · G7 estadística y figuras · G8 literatura y documentación.

- Plan detallado día por día y lista de materiales: https://claude.ai/artifact/4AcUAyhmLdQFdfkcg71r45
- Cronograma de los estudiantes por grupo, semana y horas: https://claude.ai/artifact/RT9oUAVVoAu35wmGeFATxp
