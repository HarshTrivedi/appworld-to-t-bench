FROM ghcr.io/laude-institute/t-bench/python-3-13:latest

# Install uv and setup appworld
ENV VIRTUAL_ENV=/opt/venv
RUN --mount=type=cache,target=/root/.cache/uv \
    --mount=type=bind,from=uv,source=/uv,target=/uv \
    /uv venv /opt/venv && \
    /uv pip install appworld==0.1.3;
RUN /opt/venv/bin/python -m appworld.cli install
RUN /opt/venv/bin/python -m appworld.cli download data

# Add files needed for the task
COPY task-deps/activate.py ./
COPY task-deps/cli ./cli
RUN chmod +x ./cli

# Start appworld environment server in the background
RUN nohup appworld serve environment --port 9000 --root /prohibited > nohup.out &

# Wait until server is up
RUN until curl --output /dev/null --silent --head --fail http://0.0.0.0:9000/; do \
    echo "Waiting for server to start..."; \
    sleep 1; \
done

# activate given task
RUN /opt/venv/bin/python activate.py {TASK_ID}

# Clean up files not needed anymore
RUN rm activate.py