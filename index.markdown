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

•	Empleados

Se registra la información personal de los empleados de la empresa: nombre, DNI, Teléfono, email, cargo, fecha de ingreso, dirección, distrito y estado. 

•	Contratistas

Contiene la información de los contratistas: nombre o razón social, RUC, tipo de contratista, Teléfono, email, dirección, distrito y estado. Esta tabla esta relacionada a la tabla subcontratos.

•	Segmento

Lista los tipos de segmentos al que pertenecen los tipos de clientes, esta relacionada a la tabla del mismo nombre.

•	Tipo Cliente

Lista los tipos de clientes, esta relacionada a la tabla de clientes.

•	Cliente

Contiene la información de los clientes de la empresa: nombre o razón social, RUC, Teléfono, email, fecha de registro y estado. 

•	Contratos

Almacena la información de los contratos de la empresa: cliente, empleado, nombre del proyecto, dirección, distrito, fecha de inicio, fecha de fin estimado, fecha de entrega real, monto acordado y estado.

•	Subcontratos

Almacena la información de los contratos de la empresa: contratos, contratistas, monto acordado, fecha de inicio, fecha de fin estimado y fecha de entrega real.

•	Penalidades

Se resgistran las penalidades generadas por retrasos en la entrega de los proyectos: contrato, días de retraso y monto penalidad.

•	Pagos Contratistas

Se registran los pagos efectuados a los contratistas: subcontrato, fecha de pago y comprobante de pago.

![Modelo de datos](/Imagenes/1 Capa de datos/Modelo de datos .jpg) 


## **Capa de Aplicación**

**1. Diagrama de Flujo**

El diagrama describe el flujo de trabajo digitalizado en la aplicación creada en Power Apps como solución de negocio para Innova Spacios, una empresa dedicada a la renovación de espacios comerciales, oficinas corporativas, restaurantes, cafeterías, tiendas de departamento entre otros.

El modelo de gestión se basa en la relación entre contratos con clientes finales y subcontratos con contratistas, lo que asegura control y trazabilidad de cada proyecto.

![Arquitectura de datos](/Imagenes/2 Capa de Aplicación/Diagrama de flujo.jpg)

**2. Aplicación en Power Apps**

**• Pantalla de Inicio**

![Pantalla Inicio](/Imagenes/2 Capa de Aplicación/Pantalla Inicio.jpg)

**• Pantalla de Contratos**

![contratos](/Imagenes/2 Capa de Aplicación/contratos.jpg)

**• Pantalla de Subcontratos**

![subcontratos](/Imagenes/2 Capa de Aplicación/subcontratos.jpg)

**• Pantalla de Pago contratistas**

![Pantalla Pago contratistas](/Imagenes/2 Capa de Aplicación/Pago contratistas.jpg)

**• Pantalla de Empleados**

![Pantalla de empleados](/Imagenes/2 Capa de Aplicación/empleados.jpg)

**• Pantalla de Segmento**

![Pantalla segmento](/Imagenes/2 Capa de Aplicación/segmento.jpg)

**• Pantalla de Tipo cliente**

![Pantalla Tipo cliente](/Imagenes/2 Capa de Aplicación/Tipo cliente.jpg)

**• Pantalla de Clientes**

![Pantalla cliente](/Imagenes/2 Capa de Aplicación/cliente.jpg)

**• Pantalla de Contratistas**

![Pantalla contratistas](/Imagenes/2 Capa de Aplicación/contratistas.jpg)

## **Capa de Extracción transformación y carga**

Se implementó un modelo de datos centralizado en Fabric Data Factory para garantizar la integración, transformación y disponibilidad de información clave relacionada con la gestión de contratos y subcontratos de la empresa Innova Spacios.

**1. Proceso ETL en Fabric Data Factory**

El flujo de trabajo ETL (Extract, Transform, Load) se estructuró en pipelines que permiten la importación, transformación y almacenamiento de datos.

•	Fuente de datos:
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

•	Pipeline principal (modelo de datos):

Extrae la información desde SQL Server y aplica reglas de transformación (normalización de nombres, validación de llaves, formatos de fechas, cálculo de montos).
Carga los datos en el Data Warehouse de Fabric, donde quedan disponibles para explotación en Power BI y análisis avanzados.

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

•	Pipeline adicional (reporte de contratistas):

Se diseñó un flujo específico para generar una tabla de reporte de nuevos contratos registrados en los últimos 30 días.
Esta tabla se almacena en el Lakehouse, sirviendo como dataset de referencia para reportes periódicos.

![Pipeline automatización python](/Imagenes/3 Capa de Extracción transformación y carga/Pipeline automatización python.jpg) 

## **Capa de Almacén y datos**

Data Warehouse con Fabric Warehouse y automatización e integración con Power Automate.





























## **Capa de Presentación**

Reportes con Microsoft Power Bi 
























## **Conclusiones:**

•	Automatización y eficiencia: La integración de pipelines ETL y notebooks en Python permite a Innova Spacios automatizar la generación y distribución de reportes clave (como el de nuevos contratistas), reduciendo la dependencia de procesos manuales y asegurando información confiable y disponible diariamente.

•	Escalabilidad y control centralizado: La arquitectura implementada garantiza un modelo de datos único y escalable que centraliza la información de contratos, subcontratos, pagos y contratistas, facilitando la trazabilidad completa de los proyectos y potenciando el análisis en Power BI para la toma de decisiones estratégicas.
