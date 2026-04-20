# Gestión y Registro de Inventario Automatizado

Problema:
El registro manual de productos suele generar duplicados en la base de datos, errores en la categorización de módulos y falta de sincronización entre las ventas realizadas y el stock disponible.

Solución:
Este flujo automatiza la validación y creación de inventario. Verifica en tiempo real si un producto ya existe en la base de datos, clasifica automáticamente la numeración de los módulos y asegura que solo los registros nuevos y únicos sean procesados, optimizando la integridad del catálogo de ventas.

Explicación de cada nodo
Registro de producto (Form): Captura los datos iniciales del producto (nombre, descripción, precio) enviados por el usuario. Es el punto de entrada que activa el proceso de validación.

Trae la data de productos BD (Supabase): Realiza una consulta a la tabla de inventario existente para obtener la lista de productos actuales. Sirve como punto de comparación para evitar duplicidades.

Identifica productos creados (Code): Ejecuta un script en JavaScript que filtra y organiza los nombres de los productos traídos de la base de datos. Crea una lista optimizada para facilitar la búsqueda en el siguiente paso.

Ya esta registrada? (If): Compara el nombre del producto nuevo contra la lista de productos existentes. Si encuentra una coincidencia exacta, detiene el flujo para evitar el duplicado; de lo contrario, permite el registro.

Cancelación de datos creados (Set): Limpia y formatea las variables del producto que pasó la validación. Prepara los datos finales asegurando que solo viaje la información necesaria para la creación.

Clasifica númeración modulos (Switch): Asigna el producto a un módulo o categoría específica según su numeración o reglas de negocio. Permite que el inventario esté organizado lógicamente desde su creación.

Crea Producto (Supabase): Inserta el nuevo registro validado y clasificado en la base de datos final. Es el nodo de cierre que confirma la entrada exitosa del producto al sistema.
