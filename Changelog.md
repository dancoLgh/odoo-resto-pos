# Changelog

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
