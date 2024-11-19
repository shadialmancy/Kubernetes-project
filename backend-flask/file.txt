FROM ubuntu:latest

# Install required system packages
RUN apt-get update && apt-get install -y \
    python3-pip \
    python3-venv \
    mysql-server \
    libmysqlclient-dev

# Create and activate a virtual environment
RUN python3 -m venv /venv
ENV PATH="/venv/bin:$PATH"

# Set up the working directory and add requirements.txt
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/

# Install dependencies inside the virtual environment
RUN pip install -r requirements.txt

# Copy the application code into the container
ADD . /code/

# Run the application
CMD ["python3", "backend.py"]

