---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
#title:  "Building Cloud Business Applications for Innova Espacios"


---
# **Building Cloud Business Applications for Innova Espacios**

Nuestro proyecto tiene el objetivo de implementar una solución de flujo de datos para la empresa Innova Espacios basado en las tecnologías de Microsoft Azure y Power Platform buscando integrar, transformar y automatizar la presentación de información de manera eficiente al usuario final.  

El siguiente Diagrama de Arquitectura nos muestra cómo se organizan y conectan todos los componentes del sistema.

**Arquitectura de Datos para Innova Espacios**
![Arquitectura de datos](/Imagenes/Arquitectura de datos.jpg)

**•	Origen de Datos (Data Source 01)**

Aquí se encuentran las bases de datos transaccionales o fuentes primarias de información.
A través de procesos ETL (Extract, Transform, Load), los datos se extraen y se envían hacia Azure SQL para su almacenamiento en la nube.

**•	Azure SQL**

Es la base de datos en la nube que centraliza la información proveniente de las fuentes.
Desde aquí se ejecutan procesos ETL para enviar los datos hacia el Fabric Data Warehouse.
También se integra con Power Apps para el desarrollo de aplicaciones low-code.

**•	Fabric Data Factory**

Herramienta encargada de la organización de flujos de datos y procesos ETL.
Se alimenta de pipelines, dataflows y notebooks (Python) para transformar y preparar la información antes de su carga en el Data Warehouse.

**•	Fabric Data Warehouse**

Almacén centralizado donde se consolidan los datos ya transformados y limpios.
Permite consultas analíticas y sirve como repositorio único de datos para consumo empresarial.

**•	Power BI**

Se conecta directamente al Data Warehouse para crear dashboards e informes interactivos.
Es la capa de visualización que facilita la toma de decisiones basada en datos.

**•	Power Automate**

Automatiza procesos y flujos de trabajo, integrando notificaciones o actualizaciones en Power BI.
Permite que ciertos eventos se ejecuten automáticamente.

**•	Usuario Final**

Accede a los dashboards y reportes en Power BI. Gracias a la arquitectura, recibe información confiable, actualizada y lista para la toma de decisiones estratégicas.

## **Capa de Datos**

**Descripción de la Base de Datos**

La base de datos del proceso operativo de Innova Espacios ha sido diseñada para gestionar de forma eficiente las generación de contratos, subcontratos y realización de pagos a los contratistas.

Esta base de datos está normalizada y distribuida en 9 tablas:  

**🔹Tablas Principales**

📑 **Contratos**

Almacena la información de los contratos de la empresa: cliente, empleado, nombre del proyecto, dirección, distrito, fecha de inicio, fecha de fin estimado, fecha de entrega real, monto acordado y estado.

📄​ **Subcontratos**

Almacena la información de los contratos de la empresa: contratos, contratistas, monto acordado, fecha de inicio, fecha de fin estimado y fecha de entrega real.

💳​ **Pagos Contratistas**

Se registran los pagos efectuados a los contratistas: subcontrato, fecha de pago y comprobante de pago.  

  
**🔹Tablas de Soporte**

👷 **Empleados**

Se registra la información personal de los empleados de la empresa: nombre, DNI, Teléfono, email, cargo, fecha de ingreso, dirección, distrito y estado. 

👷‍♂️**Contratistas**

Contiene la información de los contratistas: nombre o razón social, RUC, tipo de contratista, Teléfono, email, dirección, distrito y estado. Esta tabla esta relacionada a la tabla subcontratos.

 🏷️​ **Segmento**

Lista los tipos de segmentos al que pertenecen los tipos de clientes, esta relacionada a la tabla del mismo nombre.

 🔖​ **Tipo Cliente**

Lista los tipos de clientes, esta relacionada a la tabla de clientes.

🧍‍♂️ **Cliente**

Contiene la información de los clientes de la empresa: nombre o razón social, RUC, Teléfono, email, fecha de registro y estado. 

📉​​ **Penalidades**
Se resgistran las penalidades generadas por retrasos en la entrega de los proyectos: contrato, días de retraso y monto penalidad.

![Modelo de datos](/Imagenes/1 Capa de datos/Modelo de datos .jpg) 


## **Capa de Aplicación**

**1. Diagrama de Flujo**

El diagrama describe el flujo de trabajo digitalizado en la aplicación creada en Power Apps como solución de negocio para Innova Spacios, una empresa dedicada a la renovación de espacios comerciales, oficinas corporativas, restaurantes, cafeterías, tiendas de departamento entre otros.

El modelo de gestión se basa en la relación entre contratos con clientes finales y subcontratos con contratistas, lo que asegura control y trazabilidad de cada proyecto.

![Arquitectura de datos](/Imagenes/2 Capa de Aplicación/Diagrama de flujo.jpg)


**•	Inicio del proceso: selección de la acción a realizar (contrato, subcontrato, pago o modificación de tablas).**

**•	Contratos:**  
-	Registro de contratos con datos clave (proyecto, monto, dirección).
-	Validación de cliente nuevo → registro en tabla maestra.
-	Posibilidad de asociar subcontratos a cada contrato.

**•	Subcontratos:**
-	Registro de subcontratos con información del contratista, monto y plazos.
-	Validación de contratista nuevo → registro en tabla maestra.

**•	Pagos:**
-	Módulo independiente para registrar pagos asociados a contratos o subcontratos.

**•	Modificación de tablas:**
-	Transaccionales: actualizaciones en contratos, subcontratos y pagos.
-	Maestras: actualización de clientes, segmentos y empleados.

**•	Fin del proceso:**  
-   Se cierra cuando no es necesario registrar más información.


**2. Aplicación en Power Apps**

**🔹Pantalla de Inicio**

**Propósito**

Servir como punto de entrada principal para los usuarios, centralizando el acceso a todas las funcionalidades del sistema mediante una interfaz clara, visual y fácil de usar.

**Funcionalidades:**

• Presentación visual con logotipo de la empresa.  
• Botones que permiten navegar por cada pantalla de la aplicación.  

![Pantalla Inicio](/Imagenes/2 Capa de Aplicación/Pantalla Inicio.jpg)

**🔹Pantalla de Contratos**

**Propósito**

Registrar la información de los contratos y calcula la penalidad en caso haya retraso en la entrega de proyecto.

**Funcionalidades:**

• Generación de contrato id automático.  
• Lista desplegables de selección de empleado, cliente y distrito.  
• Cuadro de búsqueda por proyecto y estado.  
• Botón que lleva a pantalla de creación de nuevo cliente.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal.  
• Botón que lleva a pantalla de subcontratos.  
• Calcula los días de penalidad, monto de penalidad y el monto final.  

![contratos](/Imagenes/2 Capa de Aplicación/contratos.jpg)

**🔹Pantalla de Subcontratos**

**Propósito**

Registrar la información de los subcontratos.

**Funcionalidades:**

• Generación de subcontrato id automático.  
• Lista desplegables de selección de proyecto y contratista.  
• Cuadro de búsqueda por proyecto y contratista.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal.  

![Pantalla subcontratos](/Imagenes/2 Capa de Aplicación/subcontratos.jpg)

**🔹Pantalla de Pago contratistas**

**Propósito**

Registrar los pagos a los contratistas.

**Funcionalidades:**

• Generación de pago id automático.  
• Lista desplegables de selección de subcontratos. 
• Cuadro de búsqueda por proyecto y contratista.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal.  

![Pantalla Pago contratistas](/Imagenes/2 Capa de Aplicación/Pago contratistas.jpg)

**🔹Pantalla de Empleados**

**Propósito**

Gestionar los empleados de la empresa.

**Funcionalidades:**

• Generación de empleado id automático.  
• Lista desplegables de cargo y distrito. 
• Cuadro de búsqueda por nombre, cargo y estado.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal. 

![Pantalla de empleados](/Imagenes/2 Capa de Aplicación/empleados.jpg)

**🔹Pantalla de Segmento**

**Propósito**

Actualizar la tabla maestra segmentos.

**Funcionalidades:**

• Generación de segmento id automático.   
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal. 

![Pantalla segmento](/Imagenes/2 Capa de Aplicación/segmento.jpg)

**🔹Pantalla de Tipo cliente**

**Propósito**

Actualizar la tabla maestra tipo de clientes.

**Funcionalidades:**

• Generación de tipo cliente id automático.   
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal. 

![Pantalla Tipo cliente](/Imagenes/2 Capa de Aplicación/Tipo cliente.jpg)

**🔹Pantalla de Clientes**

**Propósito**

Gestionar los clientes de la empresa.

**Funcionalidades:**

• Generación de cliente id automático.  
• Lista desplegable de tipo cliente. 
• Cuadro de búsqueda por razón social, RUC y estado.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal. 

![Pantalla cliente](/Imagenes/2 Capa de Aplicación/cliente.jpg)

**🔹Pantalla de Contratistas**

**Propósito**

Gestionar los contratistas de la empresa.

**Funcionalidades:**

• Generación de contratista id automático.  
• Listas desplegables de tipo de contratista y distrito. 
• Cuadro de búsqueda por razón social, RUC y estado.  
• Botones de editar, eliminar y crear nuevo registro.  
• Botón de Inicio (Home) que permite al usuario regresar fácilmente a la pantalla principal. 

![Pantalla contratistas](/Imagenes/2 Capa de Aplicación/contratistas.jpg)

## **Capa de Extracción transformación y carga**

Se implementó un modelo de datos centralizado en Fabric Data Factory para garantizar la integración, transformación y disponibilidad de información clave relacionada con la gestión de contratos y subcontratos de la empresa Innova Espacios.

**1. Proceso ETL en Fabric Data Factory**

El flujo de trabajo ETL (Extract, Transform, Load) se estructuró en pipelines que permiten la importación, transformación y almacenamiento de datos.

**Fuente de datos:**
SQL Server inicial con tablas maestras y transaccionales:

•	Contratos  
•	Subcontratos  
•	Contratistas  
•	Segmento  
•	Cliente  
•	Tipo Cliente  
•	Empleados  
•	Penalidades  
•	Pagos Contratistas  
•	Calendario  

**Pipeline principal (modelo de datos):**

Extrae la información desde SQL Server y aplica reglas de transformación (normalización de nombres, validación de llaves, formatos de fechas, cálculo de montos).
Carga los datos en el **Data Warehouse de Fabric**, donde quedan disponibles para explotación en Power BI y análisis avanzados.

![Pipeline](/Imagenes/3 Capa de Extracción transformación y carga/Pipeline.jpg) 

**2. Notebooks con Python**

Los Notebooks en Fabric Data Factory cumplen un rol clave en la automatización de reportes y envío de notificaciones.

•	Generación del reporte de contratistas recientes:

Se ejecuta una consulta SQL sobre el Lakehouse para recuperar contratos registrados en los últimos 30 días. Los resultados se transforman en un DataFrame de Pandas.

•	Preparación del correo con HTML:

El DataFrame se convierte en tabla HTML para garantizar una presentación clara de la información en el correo. Se incluye encabezado, estilo y formato para facilitar la lectura de los usuarios finales.

•	Automatización del envío diario:

Con librerías como smtplib o mediante integración con servicios de correo empresarial, el Notebook envía automáticamente el reporte.

El proceso está programado para ejecutarse diariamente, asegurando que el equipo reciba información actualizada sin intervención manual.

![ython Notebook](/Imagenes/3 Capa de Extracción transformación y carga/Python Notebook.jpg) 

•	Pipeline adicional (reporte de nuevos contratos):

Se diseñó un flujo específico para generar una tabla de reporte de **nuevos contratos registrados en los últimos 30 días.**
Esta tabla se almacena en el **Lakehouse**, sirviendo como dataset de referencia para reportes periódicos.

![Pipeline automatización python](/Imagenes/3 Capa de Extracción transformación y carga/Pipeline automatización python.jpg) 

**Correo electrónico con el reporte programado diariamente**

![reporte correo](/Imagenes/3 Capa de Extracción transformación y carga/Reporte correo.jpg) 


## **Capa de Almacén y datos**
En Innova Espacios, la capa de Data Warehouse constituye la base central de nuestro ecosistema analítico. Aquí convergen los datos previamente transformados en la capa ETL —gestionada con Pipelines y Dataflows en Microsoft Fabric— para ser integrados en un Fabric Data Warehouse. Este repositorio organiza y normaliza la información, permitiendo un modelado optimizado que impulsa consultas ágiles, análisis confiables y reportes de alto valor estratégico en Power BI.

**Modelo de datos en Data Warehouse**

![modelo de datos warehouse](/Imagenes/4 Capa de Almacén y datos/modelo de datos warehouse.jpg) 

**Automatizaciones con Power Automate**
Como complemento de esta capa, en Power Automate se diseñaron dos flujos para poder gestionar notificaciones de manera eficiente y automatizada.

**1. 🔔​ Notificación de actualización exitosa automática de Datasets en Fabric (Ms Teams y Envío por correo)**

Esta automatización envía una notificación por Microsoft Teams y correo electrónico cada vez que el dataset del reporte de Power BI se actualiza exitosamente. 

**Flujo Power Automate**

![Flujo power automate 1](/Imagenes/4 Capa de Almacén y datos/Flujo Automate1.jpg) 

**Notificacion por Microsoft Teams**
![notificacion Teams 1](/Imagenes/4 Capa de Almacén y datos/notificacion Teams 1.jpg) 

**Notificación por Correo**
![notificacion correo](/Imagenes/4 Capa de Almacén y datos/notificacion correo.jpg) 

**2. 📊​ Reporte diario Power BI (Envío por correo)** 

Esta automatización genera y envía diariamente, por correo electrónico, un reporte en formato PDF de Power BI al personal previamente designado.

**Flujo Power Automate**

![Flujo power automate 1](/Imagenes/4 Capa de Almacén y datos/Flujo Automate2.jpg) 

**Notificación por Correo**
![notificacion correo](/Imagenes/4 Capa de Almacén y datos/notificacion correo 2.jpg) 


## **Capa de Presentación**

La capa de presentación, construida sobre Power BI, es el punto de acceso para los usuarios del negocio a toda la información procesada en el ecosistema de datos de Innova Espacios. Su objetivo es simplificar la complejidad de los datos y ofrecer una experiencia visual que apoye tanto el análisis operativo como las decisiones estratégicas.

**Elementos Clave:**

•	Visualización Estratégica: Evolución de ventas, proyectos y desempeño.  
•	Exploración Flexible: Filtros por tiempo, cliente o proveedor.  
•	Indicadores Clave: Servicios, ingresos y cálculo de margen.  
•	Automatización: Datos siempre actualizados con Microsoft Fabric y Power Automate.  

**Impacto en Remodelación de Interiores:**

•	Decisiones Ágiles: Métricas críticas para ingenieros, proveedores y clientes.  
•	Oportunidades de Mercado: Identificación de tendencias y necesidades del sector.  
•	Gestión Ejecutiva: Reportes claros para gerentes y responsables de proyectos.  
•	Eficiencia: Menos tiempo en reportes manuales, más foco en la obra y en el cliente.  





## **Conclusiones:**

•	La arquitectura implementada garantiza un modelo de datos único y escalable que centraliza la información de contratos, subcontratos, pagos y contratistas, facilitando la trazabilidad completa de los proyectos y potenciando el análisis en Power BI para la toma de decisiones estratégicas.  
•	La implementación de la aplicación desarrollada en Power Apps ha permitido facilitar el registro oportuno, la trazabilidad de las operaciones y la reducción de errores asociados a procesos manuales. Asimismo, la app brinda mayor agilidad en la administración de contratos y subcontratos, garantizando un control más eficiente sobre los compromisos adquiridos y el cumplimiento de los plazos de pago.   
•	La integración de pipelines ETL y notebooks en Python permite a Innova Spacios automatizar la generación y distribución de reportes clave (como el de nuevos contratos o top 20 contratistas con mayor cantidad de días de retraso), reduciendo la dependencia de procesos manuales y asegurando información confiable y disponible diariamente.
