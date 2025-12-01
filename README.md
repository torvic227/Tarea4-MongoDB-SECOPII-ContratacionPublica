# Tarea 4 – Almacenamiento y Consultas de Datos en Big Data (MongoDB)

Universidad Nacional Abierta y a Distancia – UNAD  
Programa: Ingeniería de Sistemas  
Curso: Big Data (Código 202016911)  
Actividad: Tarea 4 – Almacenamiento y Consultas de Datos en Big Data  

## Descripción del proyecto

Este repositorio contiene el código utilizado para la implementación del caso de uso
“Análisis de procesos de contratación pública en Colombia usando datos de SECOP II
(Departamento de Bolívar)”, desarrollado con la base de datos NoSQL MongoDB.

El proyecto hace parte de la Fase 2 de la Tarea 4, donde se diseñó una base de datos
documental, se implementaron consultas básicas y avanzadas, y se aplicaron operaciones
de agregación para obtener indicadores estadísticos a partir de contratos estatales.

## Estructura del repositorio

```text
Tarea4-MongoDB-SECOPII-ContratacionPublica/
├─ scripts/
│  ├─ 01_crud_contratos_secop.js
│  ├─ 02_filtros_operadores_contratos_secop.js
│  └─ 03_agregaciones_contratos_secop.js
├─ dataset/
│  └─ README_dataset.txt
└─ README.md
Requisitos
•	MongoDB Community Server (instalado localmente).
•	MongoDB Shell (mongosh) o MongoDB Compass.
•	Base de datos creada: UNAD_BIGDATA.
•	Colección: contratos_secop con los datos de SECOP II (Bolívar).
Cómo ejecutar los scripts
1.	Abrir mongosh o la consola integrada de MongoDB Compass.
2.	Seleccionar la base de datos:
3.	use("UNAD_BIGDATA");
4.	Ejecutar el contenido de los archivos ubicados en la carpeta scripts/:
o	01_crud_contratos_secop.js
Operaciones CRUD: inserciones de prueba, consultas básicas, actualizaciones y eliminaciones.
o	02_filtros_operadores_contratos_secop.js
Consultas con filtros, operadores lógicos y comparativos, expresiones regulares y combinaciones de criterios.
o	03_agregaciones_contratos_secop.js
Consultas de agregación para agrupar contratos por modalidad, entidad y tipo de documento del proveedor.
Caso de uso
El caso de uso se basa en datos de contratación pública descargados de la plataforma SECOP II,
filtrados para el departamento de Bolívar. Cada documento de la colección contratos_secop
representa un contrato e incluye, entre otros, los siguientes campos:
•	Nombre Entidad
•	Estado Contrato
•	Tipo de Contrato
•	Modalidad de Contratacion
•	TipoDocProveedor
•	Valor del Contrato 2
Estos campos permiten realizar análisis exploratorios, consultas filtradas y agregaciones
estadísticas sobre la actividad contractual de las entidades del departamento.
Autor
•	Víctor Hugo Vidal Molina
•	Estudiante de Ingeniería de Sistemas – UNAD
