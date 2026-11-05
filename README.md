Seguimiento de presupuesto CapEx y OpEx con Power Platform

Este es un caso que armé para practicar el trabajo de analista funcional: levantar la información con el cliente, entender el proceso como está hoy y proponer una solución con las herramientas de Microsoft Power Platform.

La empresa, las personas y las cifras son inventadas. Lo que quise que fuera real es la forma de trabajar.

Los mockups de la aplicación se pueden ver aquí: https://andersonleg.github.io/POWER-PLATFORM-PROJECT/

El caso

VoltaRed S.A.S. está construyendo 5 hubs de carga rápida para carros eléctricos en Bogotá. Cada hub tiene un presupuesto aprobado (AFE) de unos $800 millones.

Cada mes llegan cerca de 150 facturas, y contabilidad las revisa una por una para decidir si son inversión (CapEx) o gasto (OpEx) y a qué hub y PEP de SAP pertenecen. Eso trae varios problemas:

Más o menos el 12 % de las facturas hay que reclasificarlas después.
El informe para la junta sale unos 10 días hábiles tarde.
La revisoría fiscal encontró que no hay segregación de funciones, porque la misma persona puede pedir, recibir y aprobar.
Las reglas para clasificar estaban en varios Excel, cada uno con su versión.
Lo que hice

Hice cinco sesiones con el equipo de VoltaRed. Empecé con la gerente financiera para entender qué quería resolver. Después me senté con contabilidad a ver cómo procesan las facturas en el día a día, y hablé con proyectos y con compras. Con todo lo que salió de ahí preparé un taller con todas las áreas para tomar las decisiones que estaban pendientes.

De cada sesión dejé una minuta. Con los acuerdos del taller hice los diagramas del proceso, el modelo de datos y los mockups.

En qué orden revisarlo
Archivo	De qué se trata
Sesión 1	Entrevista con la gerente financiera
Sesión 2	Observación del proceso con contabilidad
Sesión 3	Entrevista con el gerente de proyectos
Sesión 4	Entrevista con compras
Sesión 5	Taller de decisiones con todas las áreas
Diagrama 1	Cómo se compra y se recibe en obra
Diagrama 2	Desde que llega la factura hasta que se paga
Diagrama 3	Cómo quedaría el proceso con Power Platform
Modelo de datos	Las tablas en Dataverse y cómo se relacionan
Mockups	Las pantallas de la app de obra y de la app de oficina

Las minutas están en Word, así que para leerlas hay que descargarlas.

Algunas decisiones del taller
Un hub se considera en servicio cuando el último cargador pasa las pruebas con la energía definitiva. Desde ese día cambia la forma de clasificar.
La energía que se consume en pruebas se capitaliza. Si una factura de energía cubre días antes y después de la puesta en servicio, se reparte por días.
Las facturas se clasifican línea por línea, porque una misma factura puede tener parte de inversión y parte de gasto.
No se libera ningún pago sin una aprobación registrada. Quien aprueba tiene 2 días hábiles y, si no responde, pasa a la gerente financiera.
El jefe de obra confirma lo que recibió desde el celular, aunque no tenga señal.
Los servicios que se piden con urgencia en obra se manejan con contratos marco que tienen topes por pedido y por mes.
Lo que hoy está en SAP se queda en SAP. La solución trabaja con la información en Dataverse.
La solución

Diagrama 3

Una app en Power Apps para la obra, para hacer solicitudes, pedir contra contratos marco y confirmar lo que llega.
Una app de oficina en Power Apps para contabilidad, con las facturas que el sistema no pudo clasificar solo, las reglas de clasificación, los contratos y lo que tesorería tiene por pagar.
Dataverse como base de datos, con permisos por hub y registro de cambios.
Power Automate para leer la factura electrónica, aplicar las reglas y enviar las aprobaciones por Teams.
Power BI para el seguimiento del presupuesto por hub. Esta parte la dejé fuera del primer alcance.
