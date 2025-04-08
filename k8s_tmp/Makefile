# Makefile

# Định nghĩa các file YAML
ZOOKEEPER_YAML = zookeeper.yaml
KAFKA_YAML = kafka.yaml
SCHEMA_YAML = schema.yaml
CONTROL_CENTER_YAML = control_center.yaml
POSTGRES_YAML = postgres.yaml
AIRFLOW_WEBSERVER_YAML = airflow_webserver.yaml
SCHEDULER_YAML = scheduler.yaml
SPARK_YAML = spark.yaml
#KUBERNETES_YAML = kubernetes.yaml

# Mục tiêu mặc định
all: apply

# Mục tiêu để apply tất cả các file YAML theo thứ tự
apply: apply_zookeeper apply_kafka apply_schema apply_control_center apply_postgres apply_airflow_webserver apply_scheduler apply_spark apply_kubernetes

# Các mục tiêu riêng lẻ theo thứ tự phụ thuộc
apply_zookeeper:
	@echo "Applying Zookeeper..."
	kubectl apply -f $(ZOOKEEPER_YAML)

apply_kafka: apply_zookeeper
	@echo "Applying Kafka..."
	kubectl apply -f $(KAFKA_YAML)

apply_schema: apply_kafka
	@echo "Applying Schema Registry..."
	kubectl apply -f $(SCHEMA_YAML)

apply_control_center: apply_kafka apply_schema
	@echo "Applying Control Center..."
	kubectl apply -f $(CONTROL_CENTER_YAML)

apply_postgres:
	@echo "Applying Postgres..."
	kubectl apply -f $(POSTGRES_YAML)

apply_airflow_webserver: apply_postgres
	@echo "Applying Airflow Webserver..."
	kubectl apply -f $(AIRFLOW_WEBSERVER_YAML)
	@sleep 300  # Chờ 10 giây

apply_scheduler: apply_airflow_webserver
	@echo "Applying Scheduler..."
	kubectl apply -f $(SCHEDULER_YAML)
	@sleep 300  # Chờ 10 giây

apply_spark:
	@echo "Applying Spark..."
	kubectl apply -f $(SPARK_YAML)

# apply_kubernetes:
# 	@echo "Applying Kubernetes (misc)..."
# 	kubectl apply -f $(KUBERNETES_YAML)

# Mục tiêu để xóa tất cả (nếu cần)
delete:
	@echo "Deleting all resources..."
	kubectl delete -f $(ZOOKEEPER_YAML) || true
	kubectl delete -f $(KAFKA_YAML) || true
	kubectl delete -f $(SCHEMA_YAML) || true
	kubectl delete -f $(CONTROL_CENTER_YAML) || true
	kubectl delete -f $(POSTGRES_YAML) || true
	kubectl delete -f $(AIRFLOW_WEBSERVER_YAML) || true
	kubectl delete -f $(SCHEDULER_YAML) || true
	kubectl delete -f $(SPARK_YAML) || true
	kubectl delete -f $(KUBERNETES_YAML) || true

.PHONY: all apply apply_zookeeper apply_kafka apply_schema apply_control_center apply_postgres apply_airflow_webserver apply_scheduler apply_spark apply_kubernetes delete