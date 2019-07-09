FROM python:3.7-alpine3.10

WORKDIR /app
VOLUME ["/app"]
USER 1001:1001
EXPOSE 8000

ENTRYPOINT ["python3", "-m", "http.server"]
