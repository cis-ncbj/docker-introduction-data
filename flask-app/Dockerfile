# Base image
FROM python:3
MAINTAINER Konrad Klimaszewski <konrad.klimaszewski@ncbj.gov.pl>

# Copy to the image pip requirements file
COPY requirements.txt /usr/src/app/

# Install dependencies (notice --no-cache-dir)
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . /usr/src/app

# Tell the port number the container should expose
EXPOSE 5000

# Run the command
CMD ["python", "./app.py"]
