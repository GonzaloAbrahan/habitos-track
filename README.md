# Ritmo — seguimiento de hábitos

App web personal para registrar hábitos, consultar rachas y revisar estadísticas mensuales desde cualquier dispositivo.

## Requisitos

- Python 3.10+
- Navegador web en el dispositivo que quieras utilizar.
- Para uso local: PC y dispositivo en la misma red Wi‑Fi.
- Para uso permanente: desplegar la app en un servidor con PostgreSQL.

## 1. Crear entorno

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### macOS/Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## 2. Ejecutar

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

La base SQLite `habitos.db` se crea automáticamente en local. En producción, si existe `DATABASE_URL`, se utiliza PostgreSQL.

API:
- http://127.0.0.1:8000/docs
- Desde otro dispositivo en la misma Wi‑Fi: `http://IP_DE_TU_PC:8000/docs`

## 3. Despliegue online

El archivo `render.yaml` configura el servicio web y PostgreSQL para desplegar la app en Render. Después del despliegue, abre la URL HTTPS desde el iPhone y añádela a la pantalla de inicio de Safari. No necesitas mantener el PC encendido.

Variables necesarias en producción:

- `DATABASE_URL`: la proporciona PostgreSQL.
- `HABITS_API_TOKEN`: define un token privado para acceder a los datos.

## 4. Seguridad

La API usa un token sencillo para las operaciones de registro. Antes de usarla, define la variable:

```powershell
$env:HABITS_API_TOKEN="cambia-este-token"
```

o:

```bash
export HABITS_API_TOKEN="cambia-este-token"
```

Para producción, usa HTTPS y un mecanismo de autenticación más robusto.

## Endpoints principales

- `GET /health`
- `GET /habits`
- `GET /habits/{habit_id}`
- `POST /checkins`
- `GET /checkins/today`
- `GET /checkins?date=YYYY-MM-DD`
- `GET /stats`
- `GET /stats/monthly?month=YYYY-MM`

La documentación interactiva completa está en `/docs`.
