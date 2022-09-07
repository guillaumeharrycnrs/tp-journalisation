FROM rsyslog-conteneur:latest

# Change user to root.
USER root

# Copy configuration for UDP and TCP lisntening.
COPY *.conf /etc/rsyslog.d/

# Set permissions.
RUN chown -R root:1000 /etc/rsyslog.conf /etc/rsyslog.d ; \
    chmod -R 0750 /etc/rsyslog.d ; \
    find /etc/rsyslog.conf /etc/rsyslog.d/ -type f -exec chmod 0440 {} \;

# Change back to unprivileged user.
USER 1000:1000

# Expose 2514 port for incoming connections.
EXPOSE 2514/tcp
EXPOSE 2514/udp

# Run rsyslogd in foreground with custom PID file path, since it's running under unprivileged user.
ENTRYPOINT [ "sh", "-c", "/usr/sbin/rsyslogd -n -i /srv/rsyslog/rsyslog.pid" ]