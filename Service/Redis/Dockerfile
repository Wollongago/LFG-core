FROM redis:6.0-alpine
LABEL maintainer="KycKyc"

# Copy production Configs
COPY configs/production /etc/redis

CMD [ "redis-server", "/etc/redis/redis.conf" ]