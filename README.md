# PlantSales-BI-Suite-Deteccion-de-Plantas-y-Analisis-de-Ventas-con-Django-y-SQL-Server
Solución integral desarrollada en Django que combina Inteligencia Artificial para el reconocimiento de imágenes y detección de enfermedades en plantas, con un robusto sistema de gestión comercial y Facturación Electrónica.

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
