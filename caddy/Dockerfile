# -----------------------------
# Builder stage: Compile Caddy with supported plugins
# -----------------------------
FROM caddy:2-builder AS builder

# نصب ابزار لازم
RUN apk add --no-cache git

# Build Caddy with supported plugins
RUN xcaddy build \
    --with github.com/ntk148v/caddy-logrotate \
    --with github.com/caddyserver/prometheus \
    --with github.com/greenpau/caddy-dynamic-headers

# -----------------------------
# Final stage: Minimal Alpine image
# -----------------------------
FROM caddy:2-alpine

# Copy compiled Caddy binary
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

# Create log directory
RUN mkdir -p /var/log/caddy

# Set working directory
WORKDIR /etc/caddy

# Copy Caddyfile
COPY Caddyfile /etc/caddy/Caddyfile

# Expose ports
EXPOSE 80 443

# Run Caddy
CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
