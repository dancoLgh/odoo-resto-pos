# Changelog

## V1.0.10

### Cobro dividido
- Se agregó la selección de productos y cantidades antes de cobrar una cuenta, con opción de cobrar el total completo.
- La aplicación consulta el importe de la selección antes de abrir el cobro y bloquea la división cuando ya existen pagos parciales.
- Se mejora el flujo de pagos parciales y se evita procesar respuestas de sincronización desactualizadas.

### Acceso de empleados
- Se incorporó un selector rápido de empleados desde el encabezado, sin salir de la mesa o el pedido actual.
- El cambio rápido solicita PIN, no permite seleccionar empleados sin PIN configurado y muestra bloqueos temporales ante intentos fallidos.
- La selección inicial ahora muestra el estado de la sesión de Punto de Venta y evita accesos cuando está cerrada.

### Catálogo e interfaz
- Se agregó el ordenamiento configurable de productos: predeterminado, precio ascendente, precio descendente y nombre.
- El orden seleccionado se aplica en categorías, búsqueda y la vista de todos los productos.
- Se compactaron cabeceras y buscadores, y se mejoró el comportamiento de modales durante acciones no cancelables.

### Compatibilidad
- Las funciones de cambio rápido por PIN y cobro dividido requieren actualizar el módulo backend DawnPy POS Mobile a una versión compatible.

## V1.0.9

### Acceso por PIN
- Se eliminó el envío automático al cuarto dígito: ahora se admiten PIN de hasta 12 dígitos y el usuario confirma el valor manualmente.
- Se normalizan los espacios accidentales tanto en el PIN almacenado como en el ingresado antes de compararlos.
- La aplicación muestra el error real devuelto por Odoo, como sesión expirada, POS no configurado o sesión de caja cerrada, en lugar de indicar siempre "PIN incorrecto".
- El indicador `has_pin` utiliza la misma normalización que la validación para evitar solicitudes innecesarias.

### Interfaz
- El modal de PIN ahora es desplazable y adaptable a teléfonos pequeños.
- Se agregó el botón "Confirmar PIN" y protección contra envíos simultáneos.

## V1.0.8

### Combos y Productos
- Se agregó soporte para configurar combos desde la aplicación móvil, seleccionar una opción por grupo y aplicar los recargos correspondientes.
- Se conserva la relación entre la línea principal del combo y sus componentes al guardar el pedido.
- Los componentes se muestran agrupados debajo del producto principal y no se contabilizan como productos independientes.
- Se excluyen del catálogo y de los productos más vendidos los artículos archivados o no disponibles para el POS móvil.
- Se bloquea el aumento de cantidades y la creación de combos con componentes inválidos, manteniendo la posibilidad de reducir líneas existentes.

### Pedidos y Sincronización
- La aplicación envía explícitamente las líneas eliminadas al actualizar una orden.
- El servidor preserva líneas que no fueron enviadas como eliminadas, evitando pérdidas por datos desactualizados o cambios concurrentes.

### Facturación y Configuración
- Se integró la política de facturación SIFEN para determinar cuándo facturar, asignar el cliente predeterminado cuando corresponde y devolver los datos del comprobante después del pago.
- Se restauró la configuración del cliente predeterminado del POS móvil.
- Se restauraron los campos que controlan atributos y valores ocultos en el selector de productos.

## V1.0.7

### Pedidos y Productos
- Se preservan individualmente las líneas que no deben agruparse, como productos de buffet, mediante identificadores únicos durante la edición, visualización y sincronización.
- Se conservan correctamente las notas de cada línea en pedidos, impresiones y cancelaciones, incluyendo compatibilidad con datos anteriores.
- Los controles de cantidad respetan la configuración que permite o impide agrupar un producto.
- La carga de productos y atributos ahora aísla errores por producto, mantiene un orden estable de categorías y dispone de un fallback cuando faltan campos opcionales de atributos.

### Pagos e Impresión
- Los pagos móviles utilizan el flujo nativo de procesamiento de órdenes de Odoo para generar correctamente movimientos de inventario, picking y facturación.
- La impresión remota completa los datos faltantes del cliente, incluidos RUC, teléfono, dirección y alias, antes de generar el comprobante.

### Actualizaciones Técnicas
- Se actualizó Expo a `54.0.33` y se incorporó `expo-font` con su configuración nativa.

## V1.0.6

### Reimpresión de Comprobantes
- Se agregó una pantalla para buscar y reimprimir tickets o facturas de órdenes pagadas de la sesión actual.
- La nueva pantalla es accesible desde el icono de impresión del encabezado y permite actualizar la lista antes de imprimir.
- La reimpresión obtiene una copia actualizada de la orden desde el servidor para evitar comprobantes con datos anteriores al cobro.

### Flujo Posterior al Pago
- Se agregó un botón para imprimir el ticket o la factura, según el tipo de comprobante, en la pantalla de pago exitoso.
- La configuración de impresión automática continúa disponible para imprimir inmediatamente después del cobro.
- Se conserva el identificador de la orden cobrada para enviar la impresión a la orden correcta.
- Se evita iniciar más de una impresión al mismo tiempo.
- La actualización de una orden sin apodo ya no elimina el apodo existente.

### Backend
- Se agregó un endpoint autenticado para consultar las órdenes pagadas, finalizadas o facturadas de la sesión actual.
- Las impresiones iniciadas desde la pantalla posterior al pago quedan registradas para auditoría.

## V1.0.5

### Rendimiento y Sincronización
- Se rediseñó la sincronización de pedidos para evitar bloqueos y solicitudes simultáneas.
- Las cargas se cancelan durante interacciones sensibles y el sondeo se pausa mientras el usuario selecciona productos.
- La lista de pedidos evita renderizados cuando los datos recibidos no cambiaron.
- Se optimizaron los cálculos de mesas y productos y se compactó el historial de notificaciones para reducir el uso de memoria.

### Catálogo e Interfaz
- Se agregó una vista predeterminada del menú configurable y persistente entre los modos de imágenes y lista.
- Se optimizaron tarjetas, buscador y categorías para tablet y se mejoró la resolución de las imágenes de productos.
- Se mejoró el comportamiento del teclado, el desplazamiento y el cierre de modales, especialmente en Android.

### Impresión y Órdenes
- Se agregó la opción de imprimir automáticamente después del cobro o solicitar confirmación antes de imprimir el ticket o la factura.
- Se incorporó la búsqueda y visualización del número POS de la orden.
- Las referencias de órdenes móviles utilizan un prefijo configurable y recurren a `MOB` cuando no existe configuración.
- El resultado de la impresión posterior al pago se registra en el historial de la orden para facilitar su auditoría.

## V1.0.4

### Mejoras de Usabilidad (UX)
- Selección automática de texto: se implementó `selectTextOnFocus` en todos los campos de búsqueda (Productos, Clientes, Pedidos) y en los campos de la pantalla de Login para que, al tocar un campo con texto, este se seleccione y pueda sobrescribirse al instante.
- Navegación fluida: al presionar "FINALIZAR" luego de un pago, la app vuelve automáticamente a la vista de todas las mesas, eliminando pasos innecesarios.

### Flujo de Cobro y Pagos
- Pantalla de Pago Exitoso: nueva vista de confirmación post-pago que muestra el Total Cobrado, el Monto Recibido y el Vuelto cuando aplica.
- Corrección de persistencia: la pantalla de éxito ahora permanece visible hasta que el usuario la cierre, incluso cuando se ejecuta la sincronización automática de órdenes con Odoo.

### Servicio de Actualización
- Fix `createDownloadResumable`: se resolvió el error que impedía descargar actualizaciones en algunos dispositivos Android.
- Sistema de fallback: se añadió un mecanismo que recurre a `downloadAsync` si el método principal falla para asegurar la finalización de la descarga en cualquier entorno.

## V1.0.3

### Mejoras de Interfaz (UI/UX)
- Margen de seguridad en listas: se incrementó el espacio inferior en el carrito y en el detalle de mesa para que los últimos productos no se oculten tras los botones de acción.
- Indicador de fin de lista: se añadió el texto decorativo "Fin de lista" en Menú, Carrito, Detalle de Mesa y Pedidos para mejorar la orientación del usuario.

### Precisión de Datos
- Soporte completo para decimales: las cantidades ahora usan una resolución de tres decimales, corrigiendo errores de redondeo en productos pesables (por ejemplo, Buffet por Kg) y evitando números excesivamente largos.
- Formateo inteligente: se eliminan los decimales innecesarios cuando no se requieren (por ejemplo, 1.5 en lugar de 1.500).

### Correcciones y Estabilidad
- Manejo de errores de impresión: la alerta de "Fallo de Impresión" solo se muestra cuando la impresión remota de cocina o pre-cuenta está activada en la configuración de Odoo.
- Sincronización de dependencias: se actualizaron las librerías base de Expo SDK y `@expo/vector-icons` para garantizar compatibilidad y estabilidad en compilaciones nativas de Android e iOS.
- Optimización de memoria: se corrigieron pequeñas fugas en los observadores de sincronización.

## V1.0.2

### Cambios Relevantes
- `src/services/updateService.js`: se corrigió el regex de detección de tags para que sea case-insensitive (`/^v/i`) y se añadió logging adicional para depuración.
- `src/components/UpdateChecker.js`: se añadió el flujo de actualización obligatoria con pantalla "Buscando actualizaciones...", diálogo comparando versiones, tamaño de APK, notas, barra de progreso y botones "Salir" / "Actualizar Ahora"; el botón atrás ahora cierra la app mientras la actualización es obligatoria y se muestra el aviso "La app se cerrará si no actualizas".
- `App.js`: la app ejecuta `UpdateChecker` antes de continuar al login; solo si no hay actualización disponible se avanza al flujo normal (Splash → Buscar actualización → Actualizar o continuar → Login).
- `app.json`: el `splash` usa `resizeMode: "contain"` para mostrar el logo completo.

## V1.0.1

### Cambios Realizados
- Botón "SALIR" arreglado en `WaiterSelectionScreen`.
- Botón de logout movido al pie de la pantalla como botón de ancho completo.
- Header centrado y con diseño más limpio.
- Texto cambiado de "SALIR" a "Cerrar Sesión" para mejor UX.
- Sistema de perfiles con autenticación biométrica en `LoginScreen`.
- Nuevo botón "Perfiles" en la esquina superior izquierda del login.
- `ProfileSelector`: modal que muestra todos los perfiles guardados.
- Cada perfil almacena nombre personalizado, URL de servidor Odoo, base de datos, usuario/contraseña (encriptados con `SecureStore`) y color distintivo.
- Autenticación biométrica (Face ID / Touch ID) requerida antes de usar un perfil.
- Guardar perfil actual con un toque y eliminar perfiles con long-press.

### Archivos Creados/Modificados
- `src/services/profileService.js`: servicio de gestión de perfiles.
- `src/components/ProfileSelector.js`: componente del selector de perfiles.
- `src/screens/LoginScreen.js`: integración del selector y perfiles.
- `src/screens/WaiterSelectionScreen.js`: botón de salida arreglado.
- `app.json`: agregado plugin `expo-local-authentication`.

### Cómo Funciona
1. En la pantalla de Login, toca "Perfiles" en la esquina superior izquierda.
2. Se abrirá el `ProfileSelector` mostrando los perfiles guardados.
3. Selecciona un perfil, autentícate biométricamente y continúa con el login.

## V1.0.0

- Versión inicial.
