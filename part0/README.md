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
