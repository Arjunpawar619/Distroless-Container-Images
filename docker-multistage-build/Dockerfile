# ------------------- Stage 1: Build Stage ------------------------------
FROM python:3.11 AS build-app

# Set the working directory to /app
WORKDIR /app/

# Copy the contents of the backend directory into the container at /app
COPY requirements.txt /app
COPY app.py /app
COPY templates /app/templates

# Install dependencies  and python specified in requirements.txt
RUN pip install -r requirements.txt

#------------------ Stage 2: Final Stage ------------------------------

# Use a slim Python 3.9 image as the final base image
FROM gcr.io/distroless/python3

WORKDIR /apps/

#Copy the application code from the backend-builder stage
COPY --from=build-app /app/ .
COPY --from=build-app /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

# Set the working directory to /app
ENV PYTHONPATH=/usr/local/lib/python3.11/site-packages
# Copy the built dependencies from the backend-builder stage
# COPY --from=build-app /usr/local/lib/python3.9/site-packages/ /usr/local/lib/python3.9/site-packages/

# Expose port 5000 for the Flask application
EXPOSE 5000

# Define the default command to run the application
CMD ["app.py"]


