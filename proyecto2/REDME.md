# Documentación del Proyecto MLOps

## 1. Introducción
Este proyecto implementa una infraestructura de MLOps utilizando **MLflow, MySQL, MinIO y FastAPI** para gestionar el ciclo de vida de modelos de machine learning.

## 2. Tecnologías Utilizadas
- **MLflow**: Seguimiento y gestión de experimentos.
- **MySQL**: Almacenamiento de metadatos.
- **MinIO**: Almacenamiento de artefactos.
- **FastAPI**: API para servir modelos.
- **Docker & Docker Compose**: Contenerización de los servicios.

## 3. Arquitectura
La arquitectura incluye los siguientes componentes:
1. **MLflow Server**: Administra experimentos y almacena metadatos en MySQL.
2. **MinIO**: Almacena modelos y artefactos.
3. **MySQL**: Base de datos de metadatos.
4. **FastAPI**: Expone la API para predicciones y gestiona modelos.

## 4. Configuración de Docker Compose
Ejemplo de `docker-compose.yml`:

```yaml
db:
  image: mysql:8.0
  environment:
    MYSQL_ROOT_PASSWORD: root_pass
    MYSQL_DATABASE: mlflow_db
    MYSQL_USER: mlflow_user
    MYSQL_PASSWORD: mlflow_pass
  ports:
    - "3306:3306"
  volumes:
    - mysql_data:/var/lib/mysql

minio:
  image: minio/minio
  command: server /data
  environment:
    MINIO_ROOT_USER: minioadmin
    MINIO_ROOT_PASSWORD: minioadmin
  ports:
    - "9000:9000"
    - "9001:9001"
  volumes:
    - minio_data:/data

mlflow:
  image: ghcr.io/mlflow/mlflow:v2.1.0
  environment:
    MLFLOW_TRACKING_URI: http://mlflow:5000
  ports:
    - "5000:5000"
  command: mlflow server --backend-store-uri mysql://mlflow_user:mlflow_pass@db/mlflow_db --default-artifact-root s3://mlflow/ --host 0.0.0.0
  depends_on:
    - db
    - minio

fastapi:
  image: tiangolo/uvicorn-gunicorn-fastapi:python3.8
  volumes:
    - ./app:/app
  ports:
    - "80:80"
  depends_on:
    - mlflow
```

## 5. Uso de MLflow
### Registrar un Experimento
```python
import mlflow
mlflow.set_tracking_uri("http://localhost:5000")
mlflow.set_experiment("mi_experimento")
```

### Registrar un Modelo
```python
with mlflow.start_run():
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_metric("accuracy", 0.95)
    mlflow.sklearn.log_model(modelo, "modelo")
```

### Recuperar un Modelo
```python
import mlflow.pyfunc
modelo = mlflow.pyfunc.load_model("models:/mi_modelo/1")
prediccion = modelo.predict(datos)
```

## 6. Endpoints de FastAPI
Ejemplo de `main.py` en FastAPI:
```python
from fastapi import FastAPI
import mlflow.pyfunc

app = FastAPI()
model = mlflow.pyfunc.load_model("models:/mi_modelo/1")

@app.post("/predict")
def predict(data: dict):
    return {"prediction": model.predict(data)}
```

## 7. Despliegue y Ejecución
### Iniciar Servicios
```bash
docker-compose up -d
```
### Verificar MLflow
Acceder a **http://localhost:5000**
### Probar API
```bash
curl -X POST "http://localhost/predict" -H "Content-Type: application/json" -d '{"data": [1.0, 2.0, 3.0]}'
```

## 8. Conclusión
Este proyecto proporciona una solución completa para gestión de modelos en entornos MLOps con almacenamiento, versionado y despliegue automatizado.

