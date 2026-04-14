FROM nginx:1.29-alpine

RUN apk update && \
    apk upgrade --no-cache && \
    rm -rf /var/cache/apk/*

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
