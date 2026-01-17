# Changelog

## V1.0.2

✅ Cambios Relevantes:
- `src/services/updateService.js`: se corrigió el regex de detección de tags para que sea case-insensitive (`/^v/i`) y se añadió logging adicional para depuración.
- `src/components/UpdateChecker.js`: se añadió el flujo de actualización obligatoria con pantalla "Buscando actualizaciones...", diálogo comparando versiones, tamaño de APK, notas, barra de progreso y botones "Salir" / "Actualizar Ahora"; el botón atrás ahora cierra la app mientras la actualización es obligatoria y se muestra el aviso "La app se cerrará si no actualizas".
- `App.js`: la app ahora ejecuta `UpdateChecker` antes de continuar al login; solo si no hay actualización disponible se avanza al flujo normal (Splash → Buscar actualización → Actualizar o continuar → Login).
- `app.json`: el `splash` usa `resizeMode: "contain"` para mostrar el logo completo.

## V1.0.1

✅ Cambios Realizados:
- Botón SALIR arreglado en `WaiterSelectionScreen`.
- Botón de logout movido al pie de la pantalla como botón de ancho completo.
- Header centrado y con diseño más limpio.
- Texto cambiado de "SALIR" a "Cerrar Sesión" para mejor UX.
- Sistema de Perfiles con Autenticación Biométrica en `LoginScreen`.
- Nuevo botón "Perfiles" en la esquina superior izquierda del login.
- `ProfileSelector`: Modal que muestra todos los perfiles guardados.
- Cada perfil almacena nombre personalizado, URL de servidor Odoo, base de datos, usuario/contraseña (encriptados con `SecureStore`) y color distintivo.
- Autenticación biométrica (Face ID / Touch ID) requerida antes de usar un perfil.
- Guardar perfil actual con un toque y eliminar perfiles con long-press.

Archivos creados/modificados:
- `src/services/profileService.js`: Servicio de gestión de perfiles.
- `src/components/ProfileSelector.js`: Componente del selector de perfiles.
- `src/screens/LoginScreen.js`: Integración del selector y perfiles.
- `src/screens/WaiterSelectionScreen.js`: Botón de salida arreglado.
- `app.json`: Agregado plugin `expo-local-authentication`.

📋 Cómo funciona:
1. En la pantalla de Login, toca "Perfiles" en la esquina superior izquierda.
2. Se abrirá el `ProfileSelector` mostrando los perfiles guardados.
3. Selecciona un perfil, autentícate biométricamente y continúa con el login.

## V1.0.0

Versión inicial.
