```mermaid
sequenceDiagram
    participant user as Usuario
    participant browser as Navegador
    participant server as Servidor

    Note right of user: Escribe una nota en el campo de texto

    user->>browser: Clic en el botón "Save"
    Note right of browser: El navegador previene el comportamiento por defecto del formulario

    Note right of browser: El navegador crea un objeto con el contenido de la nota y la fecha

    browser->>server: POST /new_note con el contenido de la nota en formato JSON
    activate server
    Note right of server: El servidor guarda la nota y responde con una redirección
    server-->>browser: Redirección a /notes
    deactivate server

    browser->>server: GET /notes
    activate server
    server-->>browser: HTML de la página
    deactivate server

    browser->>server: GET /main.css
    activate server
    server-->>browser: archivo CSS
    deactivate server

    browser->>server: GET /main.js
    activate server
    server-->>browser: archivo JavaScript
    deactivate server

    Note right of browser: El navegador ejecuta el JS y hace una petición para obtener las notas

    browser->>server: GET /data.json
    activate server
    server-->>browser: Lista de notas (incluyendo la nueva)
    deactivate server

    Note right of browser: El navegador ejecuta la función que muestra las notas en pantalla

