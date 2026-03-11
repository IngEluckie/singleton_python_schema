# singleton_python_schema

Implementación en Python de un **Singleton** para gestionar una conexión SQLite reutilizable desde varios scripts.

## Características
- Una sola instancia de `Database` por proceso.
- Nombre de base opcional: `Database("miniDB")`.
- Si no envías nombre, usa `systemDB.db` por defecto.
- Si el nombre no trae extensión, agrega `.db` automáticamente.
- Métodos listos para `execute_query`, `fetch_query` y `executemany`.

## Uso rápido
```python
from singleton import Database

# Base por defecto: systemDB.db
db = Database()

# Base personalizada: miniDB.db
db_custom = Database("miniDB")  # si ya existe instancia activa, reusa la actual

# Ejemplo de operación
db.execute_query("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)")
db.execute_query("INSERT INTO users (name) VALUES (?)", ("Ana",))
rows = db.fetch_query("SELECT * FROM users")
print(rows)

# Cerrar conexión
db.close_connection()
```

## Nota importante
Para cambiar de base de datos dentro del mismo proceso, primero cierra la conexión actual:

```python
db = Database("A")
db.close_connection()
db = Database("B")
```
