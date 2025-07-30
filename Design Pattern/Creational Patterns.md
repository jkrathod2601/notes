#### **Singleton Pattern**
Ensure a class has **only one instance** and provide a **global access point** to it.

###### **Real-World Example**
- **Logger class** (only one log file)
- **Database connection pool**
- **Configuration manager**

```
+-------------------+
|   Singleton       |
+-------------------+
| - instance        |  <-- Static field
| - constructor()   |  <-- Private constructor
+-------------------+
| + getInstance()   |  <-- Public static method
+-------------------+
```

```
class SingletonMeta(type):
    _instance = None

    def __call__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__call__(*args, **kwargs)
        return cls._instance

class Logger(metaclass=SingletonMeta):
    def log(self, msg):
        print(f"[LOG]: {msg}")

# Usage
logger1 = Logger()
logger2 = Logger()

print(logger1 is logger2)  # True (same instance)
```

### When to Use

- When you need **one shared resource** like:
    - Logging
    - Configurations
    - Cache
    - Thread pool