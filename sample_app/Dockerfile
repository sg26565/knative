# Use the official lightweight Python image.
# https://hub.docker.com/_/python
FROM python:3.12-slim

# switch to nonprivileged user
ENV USER python
ENV HOME /home/$USER
RUN useradd -m $USER
USER $USER

# Allow statements and log messages to immediately appear in the Knative logs
ENV PYTHONUNBUFFERED True

# Copy local code to the container image.
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY app.py ./

# Install production dependencies.
ENV PATH $HOME/.local/bin:$PATH
RUN pip install --user Flask gunicorn

# Run the web service on container startup. Here we use the gunicorn
# webserver, with one worker process and 8 threads.
# For environments with multiple CPU cores, increase the number of workers
# to be equal to the cores available.
CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 --timeout 0 app:app 