FROM golang:1.18-alpine as builder

WORKDIR /build

RUN apk update && apk add git
COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o binary


FROM scratch as prod

WORKDIR /backend
COPY --from=builder /build/binary binary

EXPOSE 8080
CMD ["/backend/binary"]
