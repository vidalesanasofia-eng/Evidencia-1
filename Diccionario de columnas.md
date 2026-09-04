

**Evidencia 1**  
**Diccionario de base de datos**  
   
**Autor**:

Ana Sofia Vidales Hinojosa A00841793

**Profesores:**   
Carlos Daniel Nolasco Cruz  
Claudia Aja Leyva

*Plataformas de analítica de negocios para organizaciones*

**Diccionario de Columnas** 

Este documento describe cada campo de la tabla de operaciones de crédito recibida del socio formador, incluyendo su significado de negocio, su relevancia para el análisis de prevención de lavado de dinero (PLD), y notas de validación pendientes.

**1\. Identificación de la entidad y del cliente**

* **Folio**: Identificador único de la operación de crédito. Es el mismo valor que folio1 (columna duplicada o generada en dos etapas del proceso). Es la llave primaria de la tabla de hechos. Debe validarse que no existan folios duplicados que representen operaciones distintas.  
* **folio1**: Duplicado de Folio. Mismo identificador de operación. Se recomienda eliminar una de las dos columnas en la fase de normalización, dejando solo Folio como llave, para evitar redundancia.  
* **Empresa**: Entidad legal bajo la cual se otorga el crédito (ej. la razón social de Spin / Compropago). Relevante si en el futuro existe más de una entidad emisora; permite segmentar operaciones por entidad regulada.  
* **RFC**: Registro Federal de Contribuyentes del cliente que solicita el crédito. Campo crítico de identificación (KYC). Es el dato que permite consolidar a un mismo cliente aunque cambie el nombre capturado, y es indispensable para el aviso a la UIF/SAT. Debe validarse el formato y que no haya RFC genéricos o inválidos.  
* **Cliente**: Nombre completo del cliente. Se debe cruzar con RFC para detectar inconsistencias (mismo RFC con nombres distintos, o mismo nombre con RFC distinto — señal de posible duplicidad o suplantación).

**2\. Estatus de la operación**

* **Status**: Estado general del crédito: Liquidado o Activo. Indica si el crédito ya se pagó en su totalidad o sigue vigente. Relevante para saber qué operaciones deben seguir monitoreando para el cálculo de acumulación.  
* **Estatus\_Cobranza**: Estado del proceso de cobranza del crédito: Liquidado o Activo. Aunque similar a Status, puede representar una vista distinta (ej. cobranza administrativa vs. estatus contable del crédito). Se debe validar con el equipo de negocio si ambas columnas son redundantes o si divergen en algunos casos (ej. un crédito con Status=Activo pero Estatus\_Cobranza=Liquidado por condonación).

**3\. Fechas del ciclo de vida del crédito**

* **Solicitud**: Fecha en que el cliente solicitó el crédito. Es la fecha base para agrupar por cohortes (clientes que iniciaron crédito en el mismo periodo) y para construir el análisis mensual.  
* **Fecha\_Deposito**: Fecha en que se depositó el efectivo del crédito al cliente. Marca el momento en que efectivamente se materializa la operación de dinero — es la fecha relevante para el cálculo de umbral por operación individual (aviso).  
* **Fecha\_de\_primer\_pago**: Fecha en que el cliente realizó (o debía realizar) su primer pago. Útil para medir el tiempo entre depósito y primer pago, y para detectar patrones de mora temprana, que combinados con desviaciones de monto pueden ser una señal adicional de riesgo.

**4\. Características del crédito**

* **loan\_name\_**: Tipo o nombre del producto de crédito otorgado (ej. distintas líneas o productos de Spin Credit). Permite segmentar el análisis por tipo de producto — importante porque cada producto puede tener un perfil de riesgo distinto.  
* **Monto**: Monto en pesos otorgado en la operación de crédito. Campo central del modelo de alertas: es el valor que se compara contra el umbral individual y el que se acumula en la ventana de 6 meses para el aviso por acumulación.  
* **Plazo**: Duración del crédito en meses (valores observados: 4, 6, 8 o 12). Junto con Monto, permite construir el perfil esperado de comportamiento del cliente (ej. detectar si un cliente que normalmente pide plazos cortos súbitamente solicita el plazo máximo con un monto alto).  
* **Tasa\_con\_impuesto**: Tasa de interés aplicada al crédito, incluyendo impuesto (IVA). Es la tasa real que paga el cliente. Relevante para calcular el costo total del crédito y el monto real que se mueve en la operación (capital \+ intereses).   
* **Tasa\_sin\_impuesto**: Tasa de interés base aplicada al crédito, antes de impuesto. Sirve como base de cálculo; la diferencia contra Tasa\_con\_impuesto debería corresponder al IVA (16%).  
* **Frecuencia**: Periodicidad de pago del crédito: Mensual o Semanal  
* **Cuota**: Monto en pesos que el cliente paga en cada periodo de pago (mensualidad o pago semanal).   
* **Cuotas**: Número de pagos o plazos correspondientes al crédito (relacionado con Plazo y Frecuencia). 

 

