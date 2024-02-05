FROM golang:1.17 AS builder

WORKDIR /app

COPY . .

RUN go get .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o docker-registry-exporter

FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/docker-registry-exporter .
EXPOSE 9055
ENTRYPOINT ["./docker-registry-exporter","--registry-address=http://registry:5000", "--listen-address=0.0.0.0:9055"]