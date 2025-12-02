FROM caddy:2-builder AS builder

RUN xcaddy build \
    --with github.com/caddyserver/caddy/v2/cmd/caddy \
    --with github.com/caddyserver/cors \
    --with github.com/caddyserver/realip \
    --with github.com/caddyserver/minify \
    --with github.com/caddyserver/security \
    --with github.com/caddyserver/logrotate \
    --with github.com/mholt/caddy-bot-detect \
    --with github.com/caddyserver/prometheus \
    --with github.com/greenpau/caddy-dynamic-headers

FROM caddy:2-alpine

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
