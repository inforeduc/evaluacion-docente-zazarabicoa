# Evaluación docente de Zazarabicoa

Aplicación web para el docente: datos personales, años y asignaturas, plan de evaluación,
notas por lapso (1, 2 y 3), importación de secciones desde Excel y exportación a PDF y Excel.

## Cómo funciona
1. Al abrir la página se pide la **clave de acceso de la institución** (la misma para todos).
2. Luego cada docente **crea su usuario** o entra con el suyo.
3. Los datos de cada docente se guardan en la nube (Firebase, proyecto `zazarabicoa-2b864`) y se ven desde cualquier equipo.
4. Las reglas de Firestore impiden que un docente lea o cambie los datos de otro.

## Publicar con GitHub Pages
1. Sube `index.html`, `README.md`, `generar-clave.html`, `firestore.rules` y `.nojekyll` a un repositorio.
2. En el repositorio entra a **Settings > Pages**, elige **Deploy from a branch**, rama **main**, carpeta **/ (root)** y pulsa **Save**.
3. La página queda en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`.
4. La página debe abrirse desde esa dirección. Abrir `index.html` como archivo en el equipo no funciona con el inicio de sesión.

## Configuración en Firebase (una sola vez)
- **Authentication > Método de acceso:** activar "Correo electrónico/contraseña".
- **Firestore Database > Reglas:** pegar el contenido de `firestore.rules` y pulsar **Publicar**.
- **Authentication > Configuración > Dominios autorizados:** agregar `TU-USUARIO.github.io` si Firebase lo pide.

## Clave de acceso de la institución
La clave inicial es `zazarabicoa123`. Para cambiarla, abre `generar-clave.html` en el navegador, escribe la nueva clave y copia la línea que aparece. Luego abre `index.html` con el Bloc de notas, busca la línea que empieza con `var ACCESS=`, reemplázala, guarda y sube el archivo a GitHub.
Esta clave detiene a quien no la tiene, pero como la página es pública no es una protección absoluta.

## Panel de administración
La pestaña **Administración** muestra la lista de todos los docentes (usuario, nombre, asignaturas, secciones, estudiantes y última actualización), permite ver y descargar en Excel o PDF los datos de cada uno, descargar la lista en Excel y eliminar los datos de un docente. Es solo lectura: el administrador no puede cambiar las notas de otros.
Para activarlo (una sola vez):
1. Sube el nuevo `index.html` a GitHub y abre la página.
2. Crea tu propio usuario en la página. Se recomienda usar tu correo como usuario.
3. En Firebase, entra a **Authentication > Usuarios** y copia el **UID de usuario** de tu cuenta.
4. En **Firestore Database > Reglas**, pega el contenido de `firestore.rules` y reemplaza `PEGA_AQUI_EL_UID_DEL_ADMINISTRADOR` por tu UID. Pulsa **Publicar**.
5. Cierra sesión y vuelve a entrar: aparece la pestaña **Administración**.
Las reglas son las que dan el permiso. Un docente común no puede ver el panel ni leer datos de otros, aunque modifique la página.

## Usuarios
- El usuario puede ser un nombre o un correo. Si usa un correo real, puede recuperar su contraseña con "Olvidé mi contraseña".
- Si un usuario con nombre (no correo) olvida su contraseña, no recibe correos de recuperación porque ese correo es interno. Debe crear un usuario nuevo, de preferencia con su correo, y restaurar su copia de seguridad. El administrador puede eliminar la cuenta anterior en **Authentication > Usuarios**.
- El administrador ve todos los docentes en la pestaña **Administración** de la página (ver abajo). También puede verlos en Firebase: **Authentication > Usuarios**, y sus datos en **Firestore > Datos > docentes**.
- La sesión se cierra sola tras 15 minutos sin actividad.
- Si se abre la misma cuenta en dos equipos a la vez, el que guardó primero gana y el otro avisa para recargar, así no se pisan los datos.

## Privacidad
Los datos de los estudiantes quedan en el proyecto de Firebase, no en GitHub. Quien administra el proyecto puede verlos en la consola de Firebase.
