FROM python:3.11-slim

WORKDIR /app

# Install system dependency required by LightGBM
RUN apt-get update && \
    apt-get install -y --no-install-recommends libgomp1 && \
    rm -rf /var/lib/apt/lists/*

# Copy and install Python dependencies
# Since Railway root is set to 'backend', we copy from the current dir
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy backend application code
COPY . .

# Start the server using the shell form to allow environment variable expansion
CMD uvicorn app.main:app --host 0.0.0.0 --port ${PORT:-8000}
