FROM python:3.12-slim

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install --no-install-recommends git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["opentelemetry-instrument", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
# RUN pip install -r requirements-dev.txt
RUN pip install --no-cache-dir \
        opentelemetry-api \
        opentelemetry-sdk \
        opentelemetry-semantic-conventions \
        opentelemetry-proto \
        opentelemetry-exporter-otlp \
        opentelemetry-exporter-otlp-proto-http \
        opentelemetry-exporter-otlp-proto-grpc
   
RUN pip install --no-cache-dir \
    opentelemetry-instrumentation \
    opentelemetry-distro \
    opentelemetry-util-http \
    opentelemetry-instrumentation-asgi \
    opentelemetry-instrumentation-httpx \
    opentelemetry-instrumentation-fastapi \
    opentelemetry-instrumentation-logging

COPY . .

EXPOSE 8000

CMD ["python", "main.py"]
