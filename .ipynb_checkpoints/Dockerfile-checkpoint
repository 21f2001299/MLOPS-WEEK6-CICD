# Use slim Python base image
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Install system-level dependencies (needed by pandas, numpy, etc.)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        gcc \
        libatlas-base-dev \
        libffi-dev \
        libpq-dev \
        curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code
COPY . .

# Expose port (for GKE or local testing)
EXPOSE 8080

# Run the FastAPI app with Uvicorn
CMD ["uvicorn", "iris_fastapi:app", "--host", "0.0.0.0", "--port", "8200"]
