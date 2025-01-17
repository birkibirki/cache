FROM python:alpine3.16

WORKDIR /app

# Install curl for healthchecks
RUN apk add curl

RUN echo "hello world"

# Create the log file
RUN touch /app/logfile.log

# Setup a nonroot user for security
RUN adduser -D nonroot
RUN chown nonroot:nonroot /app/logfile.log
USER nonroot

# Upgrade pip
RUN pip install --upgrade pip

# Install dependencies
COPY requirements.txt .
RUN pip install --user --no-cache-dir --upgrade -r requirements.txt

# Copy the app
COPY main.py /app/main.py

# Copy the log config
COPY log.ini /app/log.ini

# Copy the config
COPY config.json /app/config.json

# Expose the app's port
EXPOSE 8000

# Run the FastAPI server
ENTRYPOINT ["python", "-m"] 
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--log-config", "/app/log.ini"]
