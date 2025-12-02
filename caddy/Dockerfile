FROM caddy:2-alpine

RUN caddy add-plugin cors \
    && caddy add-plugin realip \
    && caddy add-plugin minify \
    && caddy add-plugin security \
    && caddy add-plugin logrotate \
    && caddy add-plugin bot-detect \
    && caddy add-plugin prometheus \
    && caddy add-plugin dynamic-headers
