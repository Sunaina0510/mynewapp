# FROM python:3.11-slim as build
# WORKDIR /app
# COPY requirements.txt .
# RUN pip install --no-cache-dir -r requirements.txt
# COPY . .
# CMD ["python", "app.py"]

# Stage 1 - Builder
FROM python:3.11-slim AS build

WORKDIR /app

# Install dependencies
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Copy source code
COPY . .

# Stage 2 - Final runtime image
FROM python:3.11-slim AS final

WORKDIR /app

# Copy installed Python packages from builder
COPY --from=build /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

# Copy application code
COPY --from=build /app /app

# Default command
CMD ["python", "app.py"]
