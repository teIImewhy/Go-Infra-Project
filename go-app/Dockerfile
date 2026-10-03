# ----------------- Build stage -----------------
FROM golang:1.24 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /go-app ./cmd


# ---------------- Runtime stage -----------------
FROM gcr.io/distroless/static-debian12:nonroot

WORKDIR /app

COPY --from=builder /go-app /app/go-app

EXPOSE 8000

USER nonroot:nonroot

ENTRYPOINT ["/app/go-app"]
