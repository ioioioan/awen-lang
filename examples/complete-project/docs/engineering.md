# Engineering decisions

Use plain HTML, CSS and JavaScript. Keep the implementation under src/ and tests under tests/. Store a JSON array of tasks in browser local storage. Each task needs a stable ID, text, and completion flag. Treat missing or invalid stored data as an empty list without crashing. Do not use external APIs. The execution agent may choose a minimal local test runner, but should explain any dependency introduced.
