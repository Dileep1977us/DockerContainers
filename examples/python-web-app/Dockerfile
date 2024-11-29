FROM ubuntu

# Set the working directory
WORKDIR /app

# Copy the requirements file and the devops directory into the container
COPY requirements.txt /app
COPY devops /app

# Install necessary packages and create a virtual environment
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    python3 -m venv /opt/venv

# Set the PATH to use the virtual environment's Python and pip
ENV PATH="/opt/venv/bin:$PATH"

# Upgrade pip and install required Python packages
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Set the working directory to where your Django app is located
WORKDIR /app/devops

# Specify the entry point for the container
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
