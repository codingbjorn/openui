# Stage 1: Build the virtual environment
FROM python:3.12-bookworm AS build-venv


# Copy pyproject.toml and other necessary files for building the virtual environment
COPY pyproject.toml /build/pyproject.toml


# Create a virtual environment and install the necessary packages
RUN python -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel && \
    /venv/bin/pip install /build


# Stage 2: Copy the virtual environment into a distroless image
FROM python:3.12-slim-bookworm


# Set the PATH environment variable to include the virtual environment
ENV PATH="/venv/bin:$PATH"


# Copy the virtual environment from the build stage
COPY --from=build-venv /venv /venv


# Copy the application code into the container
COPY . /app


# Set the working directory
WORKDIR /app


# Install the application dependencies
RUN pip install --no-deps -U /app


# Set the entry point to run the application
ENTRYPOINT ["python", "-m", "openui"]
