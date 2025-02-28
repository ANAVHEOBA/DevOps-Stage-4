FROM python:3.8-slim

# Install build dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        gcc \
        python3-dev \
        libffi-dev \  # Added for thriftpy2
        && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .

# Upgrade pip first
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

COPY . .
CMD ["python", "main.py"]