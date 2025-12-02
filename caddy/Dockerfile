# -----------------------------
# Builder stage: Compile Caddy with plugins
# -----------------------------
FROM caddy:2-builder AS builder

# Build Caddy with required plugins
RUN xcaddy build \
    --with github.com/greenpau/caddy-bot-detect \
    --with github.com/caddyserver/format-minify \
    --with github.com/ntk148v/caddy-logrotate \
    --with github.com/caddyserver/prometheus \
    --with github.com/greenpau/caddy-dynamic-headers

# -----------------------------
# Final stage: Minimal Alpine image
# -----------------------------
FROM caddy:2-alpine

# Copy compiled Caddy binary from builder stage
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

# Create log directory
RUN mkdir -p /var/log/caddy

# Optional: set working directory
WORKDIR /etc/caddy

# Copy your Caddyfile
COPY Caddyfile /etc/caddy/Caddyfile

# Expose ports
EXPOSE 80 443

# Run Caddy
CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
