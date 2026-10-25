# LibroLab 0.1.0

LibroLab es un MVP web abierto para crear libros infantiles, páginas para colorear y publicaciones con una experiencia editorial minimalista. Funciona en navegadores modernos de escritorio y móvil.

## Funciones implementadas

- Selección inicial de modo básico o profesional.
- Editor de páginas con título y texto editables directamente en el lienzo.
- Tipos de página: cuento, colorear, solo imagen y texto.
- Añadir, seleccionar y cambiar el orden activo de páginas mediante miniaturas; agregar nuevas páginas.
- Importación de imágenes PNG, JPG, WEBP y GIF de hasta 5 MB por imagen.
- Biblioteca creativa local de símbolos vectoriales.
- Fondos predefinidos y ajuste de tamaño del texto.
- Modo profesional con tamaño A4, Carta o cuadrado para impresión.
- Guardado automático del proyecto en `localStorage` del navegador.
- Vista previa página por página.
- Exportación a través del diálogo de impresión del navegador, con opción “Guardar como PDF”.
- PWA básica con manifiesto y service worker para recursos estáticos.
- Ayuda integrada y controles adaptables a pantallas pequeñas.

## Limitaciones conocidas

- **No hay generación de imágenes por IA integrada.** El botón “Crear con IA” construye un prompt para copiar a un servicio externo. La generación real requiere un proveedor y una clave gestionada en servidor; nunca debe exponerse una clave privada dentro de `app.js`.
- La biblioteca es una colección de símbolos vectoriales, no un catálogo extenso de ilustraciones.
- La exportación usa la función de impresión del navegador. No es todavía un motor PDF editorial dedicado y no garantiza CMYK, sangrado de imprenta, incrustación controlada de fuentes ni cumplimiento de todas las especificaciones de publicación.
- Los proyectos se guardan localmente en el navegador. No hay cuentas, nube, colaboración ni sincronización.
- No hay edición por capas, deshacer/rehacer, importación de EPUB ni formatos editables de escritorio.
- Los borradores con imágenes se guardan como datos locales; muchas imágenes grandes pueden llenar el almacenamiento disponible.
- La función PWA y el service worker requieren un contexto seguro, como HTTPS o `localhost`. Abrir `index.html` directamente no habilita todas las capacidades PWA.

## Ejecutar localmente

Requiere Python 3, Node.js no es necesario.

### Windows

Abre PowerShell en la carpeta descomprimida y ejecuta:

```powershell
py -m http.server 8080
```

Si `py` no está disponible:

```powershell
python -m http.server 8080
```

Abre `http://localhost:8080`.

### Android

Puedes subir los archivos a GitHub y activar GitHub Pages. Alternativamente, si tienes Termux con Python:

```bash
cd ruta/a/LibroLab
python -m http.server 8080
```

Abre `http://127.0.0.1:8080` en el navegador del dispositivo.

## Publicar en GitHub Pages desde Android

1. Crea un repositorio público llamado `LibroLab` en GitHub.
2. Sube el contenido de esta carpeta, manteniendo `index.html` en la raíz.
3. Abre el repositorio, entra a **Settings → Pages**.
4. En **Build and deployment**, elige **Deploy from a branch**.
5. Selecciona la rama `main` y la carpeta `/(root)`, luego guarda.
6. Espera a que GitHub Pages publique la web. La dirección suele ser `https://TU-USUARIO.github.io/LibroLab/`.
7. Prueba el sitio publicado en móvil y escritorio.

## Pruebas manuales verificables

1. Abre la app y selecciona “Crear jugando”. Debe abrirse el editor en modo básico.
2. Cambia el título del proyecto y edita el título del lienzo. Recarga la página; el proyecto debería persistir en el mismo navegador.
3. Pulsa “Añadir página”. La cuenta de páginas debe aumentar y la miniatura nueva debe seleccionarse.
4. Cambia a “Colorear”, luego a “Solo imagen” y “Texto”. El lienzo debe actualizar su presentación.
5. Sube una imagen PNG/JPG/WEBP/GIF menor de 5 MB. Debe aparecer en la página.
6. Abre “Biblioteca” y elige un símbolo. Debe cambiar el símbolo y el fondo de la página.
7. Abre “Crear con IA”. Verifica que se explica la limitación y que el prompt se prepara para copiar, sin afirmar que se genera una imagen.
8. Selecciona modo profesional y cambia el formato. El indicador del lienzo debe actualizarse.
9. Pulsa “Vista previa” y recorre las páginas.
10. Pulsa “Exportar PDF”. El navegador debe abrir la ventana de impresión. Elige “Guardar como PDF”.
11. Prueba en un móvil estrecho. El botón de menú debe desplegar la lista de páginas.
12. En GitHub Pages, recarga y verifica que los archivos estáticos se sirven por HTTPS.

## Arquitectura

- `index.html`: estructura y componentes de interfaz.
- `styles.css`: sistema visual responsive, componentes, accesibilidad y reglas de impresión visual.
- `app.js`: estado del editor, páginas, almacenamiento, biblioteca, prompts de IA, vista previa y exportación.
- `manifest.webmanifest`: metadatos de instalación PWA.
- `sw.js`: caché de recursos estáticos.
- `assets/icon.svg`: icono vectorial.

## Próximos pasos recomendados

1. Añadir pruebas automatizadas de navegador.
2. Añadir exportación/importación de proyecto JSON para copias de seguridad.
3. Mejorar accesibilidad del editor y controles de teclado.
4. Integrar un proveedor de generación de imágenes mediante un backend seguro y límites de coste.
5. Implementar un motor PDF especializado para exportación editorial real.
6. Añadir historial de cambios, deshacer/rehacer y control de resolución de imágenes.
7. Revisar permisos, licencias de imágenes y privacidad antes de distribuir a menores.

## Licencia

Este proyecto se ofrece bajo licencia MIT. Consulta `LICENSE`.
