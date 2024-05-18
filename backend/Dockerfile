FROM python:3.12-bookworm AS build-venv


# Copy the whole project directory to /build to ensure all files are available
COPY . /build


# Create a virtual environment and install the necessary packages
RUN python -m venv /venv && \
    /venv/bin/pip install --upgrade pip setuptools wheel && \
    /venv/bin/pip install /build


# Stage 2: Copy the virtual environment into a distroless image
FROM python:3.12-slim-bookworm
ENV PATH="/venv/bin:$PATH"
COPY --from=build-venv /venv /venv
COPY . /app
WORKDIR /app


# Run your application
ENTRYPOINT ["python", "-m", "openui"]
