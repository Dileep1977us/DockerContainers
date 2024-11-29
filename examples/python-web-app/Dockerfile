# Use Ubuntu as base image
FROM ubuntu:latest

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Set working directory
WORKDIR /app

# Install system dependencies (no pip installation here)
RUN apt-get update && \
    apt-get install -y \
    python3 \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Create virtual environment
RUN python3 -m venv $VIRTUAL_ENV

# Upgrade pip inside the virtual environment (use venv pip)
RUN $VIRTUAL_ENV/bin/python -m pip install --upgrade pip

# Copy project files
COPY requirements.txt /app/
COPY devops /app/devops

# Install Python dependencies inside the virtual environment
RUN $VIRTUAL_ENV/bin/python -m pip install --no-cache-dir -r requirements.txt

# Set final working directory
WORKDIR /app/devops

# Expose port for Django
EXPOSE 8000

# Set entrypoint and command
ENTRYPOINT ["python3", "manage.py"]
CMD ["runserver", "0.0.0.0:8000"]
