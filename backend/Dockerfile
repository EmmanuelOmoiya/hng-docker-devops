FROM python:latest

# Install Node.js and npm
RUN apt-get update && apt-get install -y \
    nodejs \
    npm

# Install Poetry using pip
RUN pip install poetry

WORKDIR /code/

# Copy only the necessary files
COPY ./pyproject.toml ./poetry.lock* /code/

# Install dependencies
RUN poetry install

# Copy the rest of the application
COPY . /code/

# Expose the application port
EXPOSE 8000

# Run the prestart script and start the server
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000"]