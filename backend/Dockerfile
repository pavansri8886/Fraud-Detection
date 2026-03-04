# Start from python:3.11-slim
FROM python:3.11-slim

# Set the working directory inside the container
WORKDIR /app

# Install ML dependencies at build time so they are cached as a Docker layer.
# These packages are needed by fraud_retrain_dag.py at runtime.
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy all backend files
COPY . .

# Train the model at build time
RUN python model/train.py

# Expose port 8000
EXPOSE 8000

# Launch the API with uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]