FROM frappe/bench:latest
ARG FRAPPE_URL
ARG FRAPPE_BRANCH
ARG REDIS_CACHE_URL
ARG REDIS_QUEUE_URL
ARG REDIS_SOCKETIO_URL
WORKDIR /workspace/frappe
WORKDIR /workspace/development_copy
WORKDIR /workspace/development
COPY . /workspace/frappe
USER root
RUN chown -R frappe: /workspace
USER frappe
RUN chmod +x /workspace/frappe/run.sh
RUN bench init --skip-redis-config-generation --frappe-path "$FRAPPE_URL" --frappe-branch "$FRAPPE_BRANCH" frappe-bench
WORKDIR ./frappe-bench
RUN bench set-mariadb-host mariadb
RUN bench set-redis-cache-host "$REDIS_CACHE_URL"
RUN bench set-redis-queue-host "$REDIS_QUEUE_URL"
RUN bench set-redis-socketio-host "$REDIS_SOCKETIO_URL"
# RUN cp -r /workspace/development/* /workspace/development_copy
CMD ["bench", "start"]