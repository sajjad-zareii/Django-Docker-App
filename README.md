# Django-Docker-App
# syntax=docker/dockerfile:1

# Use a lightweight Python base image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the entire application code into the working directory
COPY . .

# Install Python dependencies (ensure requirements.txt is included in your project)
RUN pip install --no-cache-dir -r requirements.txt

# Run migrations and collect static files (for production, you might handle these outside the Docker image)
RUN python3 manage.py collectstatic --noinput
RUN python3 manage.py migrate

# Expose the port that Django will run on
EXPOSE 8000

# Set the command to run the Django development server (replace with a production server in production)
CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
