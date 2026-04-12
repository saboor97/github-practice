FROM python:3.9-slim

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Optimize Python & pip behavior
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PIP_NO_CACHE_DIR=1
ENV PIP_DISABLE_PIP_VERSION_CHECK=1

WORKDIR /app

# Install system dependencies (if needed later)
RUN apt-get update && apt-get install -y \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Copy only requirements first (for caching)
COPY requirements.txt .

# Upgrade pip + install dependencies safely
RUN pip install --upgrade pip && \
    pip install --no-cache-dir --progress-bar off -r requirements.txt

# Copy app code
COPY . .

# Expose port (optional)
EXPOSE 8080

# Run app
CMD ["python", "app.py"]
