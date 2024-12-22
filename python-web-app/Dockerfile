FROM ubuntu

# Set environment variables to avoid interactive prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /app

# Copy application files
COPY requirements.txt /app
COPY devops /app

# Update and install dependencies
RUN apt-get update && \
    apt-get install -y python3 python3-venv && \
    python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install --no-cache-dir -r requirements.txt

# Set the working directory to 'devops' before running the server
WORKDIR /app/devops

# Expose the application port
EXPOSE 8000

# Define the entry point and default command
ENTRYPOINT ["/app/venv/bin/python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]