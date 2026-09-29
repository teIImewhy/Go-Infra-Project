# ----------------- Build stage -----------------
FROM golang:1.24 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /mytodo ./cmd


# ---------------- Runtime stage -----------------
FROM gcr.io/distroless/static-debian12:nonroot

WORKDIR /app

COPY --from=builder /mytodo /app/mytodo

EXPOSE 8000

USER nonroot:nonroot

ENTRYPOINT ["/app/mytodo"]
