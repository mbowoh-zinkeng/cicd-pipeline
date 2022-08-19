FROM golang:latest AS builder
RUN mkdir -p /go/src/backend
WORKDIR /go/src/backend
COPY . .

RUN GIT_TERMINAL_PROMPT=1 \
    GOARCH=amd64 \
    GOOS=linux \
    CGO_ENABLED=0 \
    go build -v --installsuffix cgo --ldflags="-s" -o backend
FROM alpine:latest

# convert build-arg to env variables
RUN apk add --no-cache tzdata
ENV TZ Africa/Lagos
RUN mkdir -p /svc/
COPY --from=builder /go/src/backend/backend /svc/

WORKDIR /svc/


CMD ["backend"]