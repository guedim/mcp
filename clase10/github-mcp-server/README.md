# 🧮 MCP Calculator Server

Este repositorio contiene un servidor basado en el **Model Context Protocol (MCP)** desarrollado en Python utilizando el framework `FastMCP`. El servidor expone herramientas matemáticas básicas (suma, resta, multiplicación y división) para ser utilizadas por clientes de IA como Claude Desktop.

---

## 🚀 Guía de Instalación y Ejecución Local

Sigue estos pasos para configurar tu entorno y probar el servidor en tu máquina.

### 1. Crear y activar el Entorno Virtual (venv)
Es vital aislar las librerías para evitar conflictos con otras instalaciones de Python.

```bash
# 1. Ve a la carpeta raíz de tu proyecto
cd /tu/ruta/al/proyecto/github-mcp-server

# 2. Crea el entorno virtual
python3 -m venv venv

# 3. Actívalo
# En macOS/Linux:
source venv/bin/activate
# En Windows:
# .\venv\Scripts\activate

```

### 2. Instalar las dependencias

Con el entorno virtual activado (verás el prefijo `(venv)` en tu terminal), instala los paquetes necesarios:

```bash
pip install mcp fastmcp

```

### 3. Configuración del Servidor (`server.py`)

Para que el protocolo MCP funcione correctamente por medio de la entrada estándar (STDIO), asegúrate de que tu archivo `src/mi_server/server.py` incluya el punto de entrada principal.

**Nota importante:** Evita usar `print()` en el código, ya que interfiere con la comunicación JSON-RPC.

```python
from mcp.server.fastmcp import FastMCP

# Inicialización de FastMCP
mcp = FastMCP("Calculadora-Pro")

@mcp.tool()
def add(a: float, b: float) -> float:
    """Suma dos números."""
    return a + b

# Asegúrate de incluir esto al final del archivo:
if __name__ == "__main__":
    mcp.run()

```

### 4. Pruebas con el MCP Inspector

El Inspector es una herramienta web para verificar que las herramientas (`tools`) estén bien registradas. Ejecuta el siguiente comando apuntando al ejecutable de Python de tu entorno virtual:

```bash
npx @modelcontextprotocol/inspector ./venv/bin/python ./src/mi_server/server.py

```

Una vez ejecutado, abre [http://localhost:3000](https://www.google.com/search?q=http://localhost:3000) en tu navegador para interactuar con el servidor.

---
