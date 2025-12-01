**01\_crud\_contratos\_secop.js**



// 01\_crud\_contratos\_secop.js

// Operaciones CRUD básicas sobre la colección contratos\_secop

// Base de datos: UNAD\_BIGDATA



use("UNAD\_BIGDATA");



// 1. Inserción de un contrato de prueba

db.contratos\_secop.insertOne({

&nbsp; "Nombre Entidad": "ENTIDAD DE PRUEBA",

&nbsp; "Nit Entidad": "999999999",

&nbsp; "Departamento": "Bogotá D.C.",

&nbsp; "Ciudad": "Bogotá",

&nbsp; "Localización": "Colombia, Bogotá D.C.",

&nbsp; "Orden": "Territorial",

&nbsp; "Sector": "No aplica/No pertenece",

&nbsp; "Rama": "Ejecutivo",

&nbsp; "Proceso de Compra": "PRUEBA-0001-2025",

&nbsp; "ID Contrato": "PRUEBA-CTO-0001",

&nbsp; "Estado Contrato": "Cerrado",

&nbsp; "Tipo de Contrato": "Prestación de servicios",

&nbsp; "Modalidad de Contratacion": "Contratación directa",

&nbsp; "Valor Contrato": 10000000,

&nbsp; "Año Firma": 2025

});



**// 2. Consultas básicas de selección**



// 2.1 Buscar contratos por nombre de entidad

db.contratos\_secop.find(

&nbsp; { "Nombre Entidad": "ALCALDÍA DEL DISTRITO TURÍSTICO Y CULTURAL DE CARTAGENA DE INDIAS" }

);



// 2.2 Buscar contratos por estado del contrato

db.contratos\_secop.find(

&nbsp; { "Estado Contrato": "Cerrado" }

);



// 2.3 Buscar contratos por tipo de documento del proveedor

db.contratos\_secop.find(

&nbsp; { "TipoDocProveedor": "NIT" }

);



// 3. Actualizaciones



// 3.1 Actualizar el valor y estado de un contrato de prueba

db.contratos\_secop.updateOne(

&nbsp; { "ID Contrato": "PRUEBA-CTO-0001" },

&nbsp; {

&nbsp;   $set: {

&nbsp;     "Valor Contrato": 15000000,

&nbsp;     "Estado Contrato": "En ejecución"

&nbsp;   }

&nbsp; }

);



// 3.2 Actualizar el estado de varios contratos por modalidad

db.contratos\_secop.updateMany(

&nbsp; { "Modalidad de Contratacion": "Contratación directa" },

&nbsp; { $set: { "Estado Contrato": "Cerrado" } }

);



// 4. Eliminaciones



// 4.1 Eliminar el contrato de prueba

db.contratos\_secop.deleteOne(

&nbsp; { "ID Contrato": "PRUEBA-CTO-0001" }

);



// 4.2 Eliminar contratos de prueba por nombre de entidad

db.contratos\_secop.deleteMany(

&nbsp; { "Nombre Entidad": "ENTIDAD DE PRUEBA" }

);



02\_filtros\_operadores\_contratos\_secop.js

// 02\_filtros\_operadores\_contratos\_secop.js

// Consultas con filtros y operadores sobre contratos\_secop



use("UNAD\_BIGDATA");



// 5.1 Buscar contratos de una entidad específica (igualdad)

db.contratos\_secop.find(

&nbsp; { "Nombre Entidad": { $eq: "ALCALDÍA DEL DISTRITO TURÍSTICO Y CULTURAL DE CARTAGENA DE INDIAS" } }

).limit(5);



// 5.2 Contratos con valor mayor a $500 millones

db.contratos\_secop.find(

&nbsp; { "Valor del Contrato 2": { $gt: 500000000 } },

&nbsp; { "Nombre Entidad": 1, "Valor del Contrato 2": 1 }

);



// 5.3 Contratos con valor entre $100 y $300 millones

db.contratos\_secop.find(

&nbsp; {

&nbsp;   "Valor del Contrato 2": {

&nbsp;     $gte: 100000000,

&nbsp;     $lte: 300000000

&nbsp;   }

&nbsp; },

&nbsp; { "Nombre Entidad": 1, "Valor del Contrato 2": 1 }

);



// 5.4 Contratos cuyo estado sea “Cerrado” o “Terminado”

db.contratos\_secop.find(

&nbsp; {

&nbsp;   $or: \[

&nbsp;     { "Estado Contrato": "Cerrado" },

&nbsp;     { "Estado Contrato": "Terminado" }

&nbsp;   ]

&nbsp; },

&nbsp; { "ID Contrato": 1, "Estado Contrato": 1 }

);



// 5.5 Filtrar contratos por modalidad que contenga la palabra “directa”

db.contratos\_secop.find(

&nbsp; { "Modalidad de Contratacion": { $regex: /directa/i } },

&nbsp; { "Modalidad de Contratacion": 1, "Nombre Entidad": 1, \_id: 0 }

).limit(10);



// 5.6 Filtrar proveedores por tipo de documento NIT o CC

db.contratos\_secop.find(

&nbsp; {

&nbsp;   "TipoDocProveedor": { $in: \["NIT", "CC"] }

&nbsp; },

&nbsp; { "Proveedor": 1, "TipoDocProveedor": 1 }

);



// 5.7 Contratos cuyo objeto incluya la palabra “obra”

db.contratos\_secop.find(

&nbsp; {

&nbsp;   "Descripcion del Proceso": { $regex: /obra/i }

&nbsp; },

&nbsp; { "ID Contrato": 1, "Descripcion del Proceso": 1 }

).limit(10);



// 5.8 Contratos donde el valor sea nulo o igual a cero

db.contratos\_secop.find(

&nbsp; {

&nbsp;   $or: \[

&nbsp;     { "Valor Contrato": { $eq: 0 } },

&nbsp;     { "Valor Contrato": { $exists: false } }

&nbsp;   ]

&nbsp; }

);



// 5.9 Contratos cuyo proveedor NO tenga NIT

db.contratos\_secop.find(

&nbsp; { "TipoDocProveedor": { $ne: "NIT" } },

&nbsp; { "Proveedor": 1, "TipoDocProveedor": 1 }

);



// 6. Filtro combinado: contratos cerrados y de modalidad directa

db.contratos\_secop.find(

&nbsp; {

&nbsp;   "Estado Contrato": "Cerrado",

&nbsp;   "Modalidad de Contratacion": "Contratación directa"

&nbsp; }

);



**03\_agregaciones\_contratos\_secop.js**



// 03\_agregaciones\_contratos\_secop.js

// Consultas de agregación sobre contratos\_secop



use("UNAD\_BIGDATA");



// 7.1 Total de contratos por modalidad de contratación

db.contratos\_secop.aggregate(\[

&nbsp; { $group: { \_id: "$Modalidad de Contratacion", total: { $sum: 1 } } },

&nbsp; { $sort: { total: -1 } }

]);



// 7.2 Top 10 entidades con mayor número de contratos

db.contratos\_secop.aggregate(\[

&nbsp; { $group: { \_id: "$Nombre Entidad", total: { $sum: 1 } } },

&nbsp; { $sort: { total: -1 } },

&nbsp; { $limit: 10 }

]);



// 7.3 Contratos por tipo de documento del proveedor

db.contratos\_secop.aggregate(\[

&nbsp; { $group: { \_id: "$TipoDocProveedor", total: { $sum: 1 } } }

]);



