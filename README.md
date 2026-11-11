# Agente de soporte con IA

Demostración en Python de un agente de soporte que consulta órdenes desde un archivo CSV, propone una respuesta con un modelo de Groq y solicita aprobación humana antes de simular el envío.

## Funcionalidades

- Busca una orden en `ordenes.csv`.
- Envía el correo del cliente y los datos de la orden a un modelo compatible con la API de OpenAI, configurado para usar Groq.
- Solicita una respuesta en formato JSON con una decisión y un borrador de correo.
- Incluye una pausa para aprobación o rechazo manual.
- Ejecuta dos escenarios de demostración: una consulta normal y un intento de prompt injection.

## Requisitos

- Python 3.
- Una clave de API de Groq válida.
- Conexión a Internet para consultar el modelo.

## Instalación

Clona el repositorio y entra en su carpeta:

```bash
git clone <URL_DEL_REPOSITORIO>
cd <NOMBRE_DEL_REPOSITORIO>
```

Crea y activa un entorno virtual. En Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

En macOS o Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

Instala las dependencias:

```bash
python -m pip install openai python-dotenv
```

## Configuración

Crea un archivo `.env` en la raíz del proyecto:

```dotenv
GROQ_API_KEY=tu_clave_de_api_de_groq
GROQ_MODEL=openai/gpt-oss-120b
```

`GROQ_MODEL` es opcional: si no se define, se usa el valor mostrado. No compartas ni subas `.env` a GitHub; el archivo está excluido mediante `.gitignore`. Si una clave se publicó o compartió por error, revócala y genera una nueva desde Groq.

## Ejecución

Desde la raíz del proyecto, con el entorno virtual activado:

```bash
python agente_soporte.py
```

El programa espera que presiones Enter para iniciar cada escenario. Para el correo normal, muestra un borrador y pide aprobación: responde `Y` para aprobar o `N` para rechazar.

## Datos de ejemplo

`ordenes.csv` contiene órdenes ficticias con estas columnas:

| Columna | Descripción |
| --- | --- |
| `id_orden` | Identificador de la orden |
| `fecha_compra` | Fecha de compra |
| `producto` | Producto comprado |
| `estado` | Estado de la orden |
| `dias_desde_compra` | Días transcurridos desde la compra |

Puedes editar el CSV para probar otras órdenes. El archivo debe conservar los encabezados y el formato esperado.

## Alcance y limitaciones

Este proyecto es una demostración educativa, no un sistema listo para producción:

- La consulta de datos es una búsqueda en CSV; no se conecta a una base de datos SQL.
- El envío del correo es simulado: no se conecta a un servicio de correo.
- La detección de prompt injection depende de instrucciones enviadas al modelo y no constituye una protección de seguridad garantizada.
- La política del prompt contempla compras de menos de 10 días y de más de 10 días; el caso de exactamente 10 días no está definido.
- Se requiere una clave de Groq para ejecutar las consultas al modelo.

No uses datos personales ni credenciales reales de clientes en esta demostración.
