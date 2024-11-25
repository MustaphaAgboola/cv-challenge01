# Step 1: Use an official Python runtime as a parent image
FROM python:3.10-slim

# Step 2: Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Step 3: Set the working directory in the container
WORKDIR /app

# Step 4: Install system dependencies (optional)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Step 5: Copy the requirements.txt file to the container
COPY requirements.txt .

# Step 6: Install Python dependencies
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Step 7: Generate the requirements.txt (from pip freeze) and save it
RUN pip freeze > requirements.txt

# Step 8: Copy the FastAPI application code to the container
COPY . .

# Step 9: Expose the port that FastAPI will run on
EXPOSE 8000

# Step 10: Run the FastAPI application using Uvicorn
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
