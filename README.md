# PlantSales-BI-Suite-Deteccion-de-Plantas-y-Analisis-de-Ventas-con-Django-y-SQL-Server
Solución integral desarrollada en Django que combina Inteligencia Artificial para el reconocimiento de imágenes y detección de enfermedades en plantas, con un robusto sistema de gestión comercial y Facturación Electrónica.

Contexto:

OLTP vs OLAP

Es crucial diferenciar entre la base de datos transaccional (OLTP) y la base de datos multidimensional (OLAP/Data Warehouse). 

Es el corazón de cualquier proyecto de Business Intelligence.

Diferenciación de Bases de Datos: Transaccional (OLTP) vs. Multidimensional (OLAP)


1. Base de Datos Transaccional (OLTP - Online Transaction Processing)


Propósito: Almacenar y gestionar las operaciones diarias y en tiempo real de tu aplicación. Es donde se registran las transacciones individuales.
Diseño: Orientado a la normalización para asegurar la integridad de los datos, minimizar la redundancia y optimizar las operaciones de inserción, actualización y eliminación.

La Solucion de la base de datos de Django, con tablas Planta, Enfermedad, AnalisisImagen, Producto, Cliente, Venta, DetalleVenta.
Tecnología Recomendada: Un RDBMS robusto y escalable, capaz de manejar muchas transacciones concurrentes.

Base de datos OLTP principal para las ventas y la factura electrónica. También podría ser la base de datos transaccional para el detector de plantas.

Ventajas de SQL Server 2008 como OLTP: Robustez, seguridad, capacidad de manejar grandes volúmenes de transacciones, características empresariales.

Configuración: Como ya mencionamos, usarías mssql-django y el driver ODBC para conectar tu aplicación Django a SQL Server 2008.

¿Y SQLite para OLTP? SQLite es una base de datos embebida, ligera y basada en archivos.

Usos comunes en Django: Es excelente para prototipos, desarrollo local, aplicaciones pequeñas con baja concurrencia o como base de datos de respaldo simple.

Limitaciones para OLTP de Ventas/Factura Electrónica: No está diseñada para entornos multiusuario con alta concurrencia o grandes volúmenes de transacciones. Su rendimiento decaería rápidamente, y carece de muchas características de seguridad y gestión de bases de datos empresariales que SQL Server 2008 ofrece.

2. Base de Datos Multidimensional (OLAP - Online Analytical Processing) / Data Warehouse


Propósito: Almacenar datos históricos de múltiples fuentes para análisis complejos, generación de informes y apoyo a la toma de decisiones. No está diseñada para transacciones en tiempo real.
Diseño: Orientado a la desnormalización (esquema en estrella o copo de nieve) para optimizar el rendimiento de las consultas analíticas que agregan grandes volúmenes de datos.

Modelar tablas FactVentas, DimFecha, DimCliente, DimProducto, DimPlanta diseñadas para BI.
Tecnología Recomendada: Un RDBMS diseñado para cargas de trabajo analíticas (aunque SQL Server es un híbrido capaz), o plataformas específicas de Data Warehouse.

SQL Server 2008 es una excelente opción para construir tu Data Warehouse y tus cubos OLAP.
Ventajas de SQL Server 2008 para OLAP/DW:

SSIS (Integration Services): Herramienta robusta de ETL para extraer datos de tu OLTP (incluyendo el de Django), transformarlos y cargarlos en tu DW.


SSAS (Analysis Services): Te permite crear cubos OLAP a partir de tu DW, proporcionando un rendimiento excepcional para consultas multidimensionales y agregaciones precalculadas.


SSRS (Reporting Services): Para la creación de informes y dashboards visuales basados en los datos del DW o los cubos.
Escalabilidad: Puede manejar grandes volúmenes de datos históricos.

Manejo de Transacciones: Aunque sea un servidor de transacciones, para DW, las transacciones se realizan en el momento de la carga de datos (ETL) y no en el momento de la consulta.


🌿 PlantSales BI Suite

Solución integral desarrollada en Django que combina Inteligencia Artificial para el reconocimiento de imágenes y detección de enfermedades en plantas, con un robusto sistema de gestión comercial y Facturación Electrónica.

## 🎯 Objetivo Principal
Diseñar e implementar una arquitectura de bases de datos diferenciada:
*   **🔄 Base de Datos Transaccional (OLTP):** Optimizada para operaciones diarias, ventas y registro de datos en tiempo real.
*   **📊 Base de Datos Multidimensional (OLAP / Data Warehouse):** Diseñada específicamente para Business Intelligence, análisis histórico y toma de decisiones.

## 🛠 Tecnologías y Arquitectura
*   **Backend:** Python | Django
*   **IA y Visión Artificial:** TensorFlow / Keras (Reconocimiento de imágenes)
*   **BD Transaccional:** SQL Server 2008 / SQLite
*   **BD Analítica / BI:** SQL Server 2008 (Data Warehouse)
*   **Herramientas BI:** SSIS (ETL), SSAS (Cubos OLAP), SSRS (Reporting Services)

## 📂 Estructura Conceptual
El proyecto demuestra la separación de responsabilidades:
1.  **App Django:** Lógica de negocio, interfaz de usuario y conexión a la BD Operativa.
2.  **Modelo Relacional:** Tablas normalizadas para Ventas, Productos, Clientes y Diagnóstico de Plantas.
3.  **Data Warehouse:** Esquema en Estrella/Copo de Nieve para análisis de Ventas y Métricas de Uso.
4.  **Integración:** Procesos ETL para migrar datos del entorno operativo al analítico.

---
*Proyecto educativo y funcional enfocado en buenas prácticas de desarrollo y arquitectura empresarial.*
<img width="744" height="1118" alt="image" src="https://github.com/user-attachments/assets/d5a8f14c-afdd-4acb-9cbc-b66066bf449f" />



[Modelo Arquitectura BI](diagrams/arquitectura.png)


Consideraciones clave para tu implementación:

Instancia de SQL Server: Puedes tener ambas bases de datos (OLTP y DW) en la misma instancia de SQL Server 2008, o en instancias separadas si la carga es muy alta. Para empezar, una sola instancia es suficiente.

Mantenimiento de ETL: Los paquetes SSIS deben ejecutarse periódicamente (ej. cada noche, cada semana) para actualizar el Data Warehouse con los nuevos datos del OLTP.

Datos del Detector para BI: Si quieres analizar los datos del detector de plantas, crearías otra "tabla de hechos" en tu Data Warehouse (ej. FactAnalisisPlantas) con sus dimensiones correspondientes (DimPlanta, DimEnfermedad, DimUsuario, DimFecha).

Al diferenciar claramente estas dos bases de datos y sus propósitos, te aseguras de que tu aplicación Django funcione de manera eficiente (OLTP) mientras construyes una plataforma robusta para el análisis de negocios (OLAP/DW) con las herramientas de SQL Server 2008.
