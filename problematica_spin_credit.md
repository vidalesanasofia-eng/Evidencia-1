# Problemática — Reto Spin Credit (OXXO / FEMSA)

## Contexto

Spin Credit se encuentra en fase de **prueba piloto** de préstamos de dinero, con miras a expandir este servicio como una nueva línea de negocio dentro del ecosistema financiero de OXXO. El otorgamiento de crédito, sin embargo, no es una operación libre de riesgo regulatorio: al mover dinero entre la empresa y sus clientes, Spin Credit adquiere obligaciones legales en materia de **prevención de lavado de dinero (PLD)**, conforme a la Ley Federal para la Prevención e Identificación de Operaciones con Recursos de Procedencia Ilícita (LFPIORPI).

## ¿Qué es el lavado de dinero y por qué es relevante aquí?

El lavado de dinero es el proceso mediante el cual una persona o red intenta **dar apariencia de legalidad a recursos de origen ilícito**, introduciéndolos al sistema financiero formal a través de operaciones aparentemente normales (depósitos, préstamos, transferencias) para después poder usarlos sin levantar sospechas.

En el caso de una institución que otorga crédito, como Spin Credit, el riesgo no es que la empresa "lave dinero" activamente, sino que **su producto sea utilizado como vehículo** por terceros para:
- Solicitar préstamos con montos elevados o atípicos que no corresponden al perfil económico del cliente.
- Fraccionar operaciones para evitar superar los umbrales que obligan a reportar.
- Usar identidades múltiples o relacionadas para mover recursos de forma coordinada.

Por eso la ley obliga a las entidades que realizan este tipo de operaciones a **vigilar, identificar y reportar** cualquier operación que se salga de lo esperado.

## El problema central

Actualmente, Spin Credit **no cuenta con un mecanismo automatizado y sistemático** para:

1. **Identificar plenamente a sus clientes** (KYC) y consolidar su información en un solo perfil confiable.
2. **Conocer y validar la actividad económica** a la que se dedica cada cliente, para poder contrastarla contra el monto y comportamiento de sus créditos.
3. **Detectar operaciones que rebasan el umbral regulatorio individual** — por ejemplo, préstamos que alcanzan o superan montos de referencia como **$188,282 MXN**, cifra que en la práctica ha servido como disparador de atención dentro del piloto.
4. **Identificar acumulación de operaciones** de un mismo cliente a lo largo de una ventana de tiempo (típicamente 6 meses), que en conjunto superen el umbral aunque cada operación individual no lo haga.
5. **Generar y dar seguimiento a los avisos** que deben enviarse a la Unidad de Inteligencia Financiera (UIF) a través del área legal, así como conservar evidencia (acuses de envío) de que dicho reporte se realizó en tiempo y forma.

Toda esta información hoy vive dispersa entre el sistema operativo de créditos (**Mambu**), el área legal y procesos manuales, sin un tablero centralizado que permita al negocio **visualizar, monitorear y anticipar** estas situaciones antes de que se conviertan en incumplimientos.

## Consecuencia de no resolverlo

Sin un sistema analítico que cruce **clientes, montos, plazos y fechas** de forma sistemática:

- Existe el riesgo de **no detectar a tiempo** operaciones o acumulaciones que debieron reportarse, exponiendo a la empresa a sanciones regulatorias.
- El área legal depende de procesos manuales o reactivos para generar avisos, lo cual no escala si el negocio de crédito crece como está planeado.
- El negocio pierde visibilidad sobre patrones de comportamiento de sus clientes (por cohorte, por periodo de originación, por monto/plazo) que serían valiosos tanto para cumplimiento como para la toma de decisiones de negocio.

## Objetivo del reto

Diseñar una solución analítica (Power BI) que, a partir de los datos que genera Mambu, permita:

- Identificar operaciones de crédito por cliente, monto y plazo.
- Detectar desviaciones respecto al comportamiento esperado (por cliente y por cohorte).
- Generar alertas automáticas para los dos tipos de aviso: **por operación individual** y **por acumulación**.
- Dar trazabilidad al proceso completo: desde la detección hasta el envío del aviso a la UIF y su acuse correspondiente.
- Visualizar esta información de forma mensual, agrupando a los clientes por el periodo en que iniciaron su crédito (análisis de cohortes).

---
*Nota: el monto de $188,282 MXN se toma como referencia operativa mencionada en el piloto. Se recomienda validarlo contra el umbral vigente en UMAs establecido por la LFPIORPI para este tipo de actividad vulnerable, ya que dicho valor se actualiza periódicamente.*
