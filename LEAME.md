<p align="center">
    <a href="https://mylisterhub.com" target="_blank">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/logo.svg" width="75" alt="Logo" style="padding-right: 5px;">
        <img src="https://raw.githubusercontent.com/FmTod2/skill-assessment/7ff556c2bb35948c7ee4e23667191ed05d8f88f3/assets/company.svg" width="400" alt="MyListerHub" style="padding-bottom: 2px;">
    </a>
</p>

<p align="center">
    <a href="https://github.com/FmTod/">Guidelines</a>
</p>

<p align="center">
    <a href="https://forms.gle/gSqn6SE3Wa65b3bS7">Questionnaire</a>
</p>

<p align="center">
    <a href="./README.md">Inglés / English</a>
</p>

# Evaluación de Habilidades

Paquete de Interacción con API de Citas con Limitación de Tasa, Caché y UI en Vue.js

## Objetivo

Evaluar tu habilidad para diseñar, desarrollar, probar y documentar un paquete completo de Laravel que consuma datos de citas de la API `https://dummyjson.com/quotes`, implemente limitación de tasa de solicitudes, utilice caché local con recuperación eficiente mediante búsqueda binaria, y proporcione una interfaz de usuario (UI) preconstruida y publicable, construida con Vue.js, para interactuar con la API.

## Tarea

Desarrollar un paquete de Laravel que simplifique la interacción con la API pública `https://dummyjson.com/quotes`. El paquete debe incluir la interacción con la API, limitación de tasa, caché y una interfaz de usuario construida con Vue.js para mostrar las citas. Los artefactos de compilación de la UI deben ser publicables para su personalización.

> [!IMPORTANT]
> El repositorio debe seguir la estructura común para paquetes de Laravel, no debe ser una aplicación.

> [!IMPORTANT]
> Todos los requisitos deben completarse para que la evaluación sea considerada. Esto no es opcional.

## Entregables

*   Un enlace a un repositorio Git público que contenga el código completo del paquete Laravel.
*   Un archivo `README.md` en el directorio raíz del paquete con instrucciones claras para la instalación, configuración, uso básico, limitación de tasa, caché y acceso/publicación de la UI en Vue.js.

## Requisitos

1.  **Estructura del Paquete:**
    *   Seguir las convenciones estándar de desarrollo de paquetes de Laravel.
    *   Incluir un proveedor de servicios (`service provider`) para registrar la funcionalidad del paquete, las rutas y los assets publicables.
    *   Incluir la estructura de directorios necesaria para tu aplicación Vue.js (por ejemplo, `resources/js`, `resources/views`).

2.  **Servicio de Cliente API:**
    *   Crear un servicio dentro del paquete que maneje la comunicación con la API `https://dummyjson.com/quotes` utilizando el cliente HTTP de Laravel.
    *   Este servicio debe incorporar lógica de limitación de tasa de solicitudes y caché local con búsqueda binaria.

3.  **Configuración:**
    *   Proporcionar un archivo de configuración para el paquete (por ejemplo, `config/quotes.php`).
    *   El archivo de configuración debe permitir a los usuarios definir:
        *   La URL base de la API (por defecto, `https://dummyjson.com`).
        *   El número máximo de solicitudes permitidas por ventana de tiempo (por ejemplo, por minuto).
        *   La duración de la ventana de tiempo en segundos (por ejemplo, 60 para un minuto).

4.  **Métodos de Interacción con la API:**
    *   `getAllQuotes()`: Obtiene todas las citas del endpoint `/quotes`.
    *   `getRandomQuote()`: Obtiene una cita aleatoria del endpoint `/quotes/random`.
    *   `getQuote(int $id)`: Obtiene una cita específica por su ID del endpoint `/quotes/{id}`. Este método debe primero verificar la caché local usando búsqueda binaria.

5.  **Implementación de la Limitación de Tasa:**
    *   Implementar un mecanismo para rastrear el número de solicitudes realizadas a la API dentro de la ventana de tiempo configurada.
    *   Si se excede el límite, pausar la ejecución durante un breve período hasta que se restablezca la ventana y luego volver a intentar la solicitud.

6.  **Caché Local con Recuperación Eficiente:**
    *   Implementar un mecanismo de caché local (por ejemplo, un array) para almacenar las citas obtenidas.
    *   El método `getQuote(int $id)` debe primero verificar esta caché.
    *   **Si la cita con el ID dado se encuentra en la caché, recuperarla usando búsqueda binaria (asumiendo que los datos en caché están ordenados por ID) y devolverla sin realizar una llamada a la API.**
    *   Si la cita no está en la caché, realizar una llamada a la API, almacenar la cita obtenida en la caché (asegurando que la caché permanezca ordenada por ID para la búsqueda binaria) y luego devolverla.

7.  **Rutas API del Paquete:**
    *   Definir rutas API dentro de tu paquete (registradas a través del proveedor de servicios, probablemente bajo un prefijo `/api/quotes`) que tu aplicación Vue.js pueda consumir. Estas rutas deben:
        *   `/api/quotes`: Devolver todas las citas.
        *   `/api/quotes/random`: Devolver una cita aleatoria.
        *   `/api/quotes/{id}`: Devolver una cita específica por ID.
    *   Crear controlador(es) dentro de tu paquete para manejar estas rutas API e interactuar con tu servicio de cliente API.

8.  **Interfaz de Usuario en Vue.js:**
    *   Construir una interfaz de usuario utilizando Vue.js dentro de tu paquete. Esta UI debe permitir a los usuarios:
        *   Ver todas las citas (potencialmente con paginación).
        *   Ver una cita aleatoria.
        *   Ver una cita específica por ID.
    *   Esta UI debe realizar solicitudes API al backend de tu paquete para obtener los datos.

9.  **Servir la Aplicación Vue.js:**
    *   Definir una ruta en tu paquete (por ejemplo, `/quotes-ui`) que sirva el punto de entrada principal de tu aplicación Vue.js. Necesitarás configurar Vite dentro de tu paquete para compilar la aplicación Vue.js en assets estáticos.

10. **Assets Publicables:**
    *   Configurar el proveedor de servicios de tu paquete para que los assets compilados de la aplicación Vue.js (por ejemplo, la carpeta `dist` que contiene JavaScript y CSS) sean publicables en la aplicación Laravel principal usando el comando `php artisan vendor:publish`. Los assets publicados deben residir en un directorio lógico dentro del directorio `public` de la aplicación principal (por ejemplo, `public/vendor/nombre-de-tu-paquete`).

11. **Uso:**
    *   Incluir instrucciones sobre cómo instalar el paquete, configurarlo y **cómo acceder a la UI preconstruida de Vue.js (la ruta definida, por ejemplo, `/quotes-ui`).**
    *   Proporcionar instrucciones claras sobre **cómo publicar los assets de la UI de Vue.js** si un desarrollador desea personalizar el frontend. Incluir pasos sobre dónde se publican los assets y cómo se pueden modificar.

12. **Pruebas:**
    *   Incluir pruebas unitarias para el servicio de cliente API.
    *   Incluir pruebas de características básicas para las rutas API de tu paquete para asegurar que devuelvan los datos correctos.

13. **Documentación:**
    *   El archivo `README.md` debe incluir documentación completa para todas las características, incluyendo instrucciones claras sobre cómo acceder y publicar la UI de Vue.js y cualquier paso de compilación necesario (por ejemplo, ejecutar `npm install` y `npm run build` dentro del directorio de la UI del paquete).

## Instrucciones de Entrega

1.  Crear un nuevo repositorio público en una plataforma como GitHub, GitLab o Bitbucket.
2.  Desarrollar el paquete Laravel de acuerdo con los requisitos descritos anteriormente.
3.  Asegurarse de que todas las pruebas pasen y que la documentación esté completa.
4.  Enviar el enlace del repositorio al(a los) evaluador(es) designado(s).

¡Buena suerte!
