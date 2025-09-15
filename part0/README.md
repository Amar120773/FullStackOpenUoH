    04
    
    sequenceDiagram
    participant client_browser as Client Browser
    participant web_server as Application Server

    Note right of client_browser: User has the /notes page open and adds a new note.
    client_browser->>web_server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate web_server
    Note left of web_server: Server receives the note text (form data), adds it to data, and instructs browser to reload.
    web_server-->>client_browser: HTTP 302 Redirect to /exampleapp/notes
    deactivate web_server

    Note right of client_browser: Browser receives the redirect and begins a full page refresh by requesting the specified page.

    client_browser->>web_server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate web_server
    server-->>client_browser: HTML document
    deactivate web_server

    client_browser->>web_server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate web_server
    server-->>client_browser: main.css
    deactivate web_server

    client_browser->>web_server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate web_server
    server-->>client_browser: main.js
    deactivate web_server

    Note right of client_browser: Browser executes the JS code, which requests the data.

    client_browser->>web_server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate web_server
    server-->>client_browser: Updated JSON data (including the new note)
    deactivate web_server

    Note right of client_browser: Browser executes callback, rendering the complete list of notes.


    05.

    sequenceDiagram
    participant user_device as User's Browser
    participant backend_api as Server Backend

    Note right of user_device: User navigates to the Single-Page App (SPA) URL.
    user_device->>backend_api: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate backend_api
    backend_api-->>user_device: HTML document
    deactivate backend_api

    user_device->>backend_api: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate backend_api
    backend_api-->>user_device: the CSS file
    deactivate backend_api

    user_device->>backend_api: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate backend_api
    backend_api-->>user_device: the SPA JavaScript file
    deactivate backend_api

    Note right of user_device: Browser executes the SPA application logic (spa.js),<br/>which immediately requests the notes data.

    user_device->>backend_api: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate backend_api
    backend_api-->>user_device: JSON data (list of notes)
    deactivate backend_api

    Note right of user_device: The JS application receives the JSON data and renders the notes onto the page dynamically.

    06.

    
