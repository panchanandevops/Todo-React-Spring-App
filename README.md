# Todo-React-Spring-App

Below are the `curl` commands to create, retrieve, update, and delete todos using your API.

### 1. Create 3 Todos
```bash
curl -X POST http://localhost/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Buy groceries"}'

curl -X POST http://localhost/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Walk the dog"}'

curl -X POST http://localhost/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Read a book"}'
```

### 2. Get All Todos
```bash
curl -X GET http://localhost/api/todos
```

### 3. Update One of the Todos (e.g., "Walk the dog")
Let's assume the ID of the "Walk the dog" todo is `12345abcd`.
```bash
curl -X PUT http://localhost/api/todos/12345abcd \
-H "Content-Type: application/json" \
-d '{"title": "Walk the dog", "completed": true}'
```

### 4. Get the Updated Todo by ID
```bash
curl -X GET http://localhost/api/todos/12345abcd
```

### 5. Delete the Updated Todo
```bash
curl -X DELETE http://localhost/api/todos/12345abcd
```

You can replace `12345abcd` with the actual ID returned from the API after creating or retrieving the todos.