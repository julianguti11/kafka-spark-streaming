# kafka-spark-streaming
Este proyecto implementa un sistema de streaming usando Apache Kafka y PySpark Structured Streaming, simulando el flujo de datos de viajes urbanos en Colombia.
# Kafka-Spark Streaming

Este proyecto demuestra un flujo de datos en **tiempo real** utilizando **Kafka** como sistema de mensajería y **Spark Streaming** para procesar los datos.  

Se utiliza un **dataset propio** simulado que genera información de viajes en ciudades de Colombia, con el número de pasajeros y el tipo de transporte.

---

## 1. Dataset propio

El dataset no es real, sino generado aleatoriamente por el productor Kafka. Cada registro tiene la siguiente estructura:

| Campo       | Tipo    | Descripción                              |
|------------|--------|------------------------------------------|
| ciudad     | string | Ciudad de Colombia donde se realiza el viaje (Bogotá, Medellín, Cali, Barranquilla) |
| tipo       | string | Tipo de transporte (Bus, Taxi, Buseta)   |
| pasajeros  | int    | Número de pasajeros en ese viaje         |
| hora       | string | Fecha y hora del registro                 |

**Ejemplo de registro generado por el productor:**

```json
{
  "ciudad": "Bogotá",
  "tipo": "Bus",
  "pasajeros": 23,
  "hora": "2025-10-21 18:50:00"
}

2. Estructura del proyecto
kafka-spark-streaming/
│
├── productor/
│   └── kafka_producer.py       # Código del productor Kafka
│
├── consumidor/
│   └── spark_consumer.py       # Código del consumidor Spark Streaming
│
├── README.md                   # Este archivo
└── requirements.txt            # Dependencias de Python

3. Configuración del entorno
Clonar el repositorio:
git clone https://github.com/julianguti11/kafka-spark-streaming.git
cd kafka-spark-streaming

Crear un entorno virtual (opcional pero recomendado):
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

Instalar dependencias:
pip install -r requirements.txt

4. Ejecutar el proyecto
4.1 Iniciar Kafka

Asegúrate de tener Kafka y Zookeeper corriendo:
4.1 Iniciar Kafka
# Iniciar Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Iniciar Kafka
bin/kafka-server-start.sh config/server.properties


4.2 Crear el topic viajes (solo la primera vez)
bin/kafka-topics.sh --create --topic viajes --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

4.3 Ejecutar el productor
python productor/kafka_producer.py

4.4 Ejecutar el consumidor
spark-submit \
  --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.6 \
  spark1_streaming_consumer.py

El consumidor mostrará en consola:
Conteo de eventos por ciudad
Promedio de pasajeros por tipo de transporte

6. Licencia

Este proyecto es para fines educativos.
