# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Set environment variables for Python
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /app

# Copy just the requirements file and install dependencies first
# This leverages Docker's layer caching for faster builds
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of your backend application code
COPY . .

# Expose the port the backend runs on
EXPOSE 8000

# Command to run the FastAPI application using Uvicorn
# This is the standard way to run FastAPI in production
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
