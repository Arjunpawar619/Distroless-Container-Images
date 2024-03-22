# ------------------- Stage 1: Build Stage ------------------------------
FROM ubuntu as build-app

# Set the working directory to /app
WORKDIR /app

# Copy the contents of the backend directory into the container at /app
COPY . .

# Install dependencies  and python specified in requirements.txt
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install --no-cache-dir -r requirements.txt

#------------------ Stage 2: Final Stage ------------------------------

# Use a slim Python 3.9 image as the final base image
FROM gcr.io/distroless/python3

WORKDIR /app

#Copy the application code from the backend-builder stage
COPY --from=build-app /app .

# Set the working directory to /app

# Copy the built dependencies from the backend-builder stage
# COPY --from=backend-builder /usr/local/lib/python3.9/site-packages/ /usr/local/lib/python3.9/site-packages/

# Expose port 5000 for the Flask application
EXPOSE 5000

# Define the default command to run the application
CMD ["python", "app.py"]
