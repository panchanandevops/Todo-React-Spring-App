Below are the `curl` commands to create, retrieve, update, and delete todos using your API.

### 1. Create 3 Todos
```bash
curl -X POST http://panchanandevops.com:30452/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Buy groceries"}'

curl -X POST http://panchanandevops.com:30452/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Walk the dog"}'

curl -X POST http://panchanandevops.com:30452/api/todos \
-H "Content-Type: application/json" \
-d '{"title": "Read a book"}'
```

### 2. Get All Todos
```bash
curl -X GET http://panchanandevops.com:30452/api/todos
```

### 3. Update One of the Todos (e.g., "Walk the dog")
Let's assume the ID of the "Walk the dog" todo is `66c5f330f7161450c878b844`.
```bash
curl -X PUT http://panchanandevops.com:30452/api/todos/66c5f330f7161450c878b844 \
-H "Content-Type: application/json" \
-d '{"title": "Walk the dog", "completed": true}'
```

### 4. Delete the Updated Todo
```bash
curl -X DELETE http://panchanandevops.com:30452/api/todos/66c5f330f7161450c878b844
```

You can replace `66c5f330f7161450c878b844` with the actual ID returned from the API after creating or retrieving the todos.