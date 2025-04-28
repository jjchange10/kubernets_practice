# ビルドステージ
FROM golang:1.24.2-alpine AS builder

WORKDIR /app

# Goモジュールがある場合は go.mod, go.sum を先にコピー
COPY go.mod ./

# ソースコードをコピー
COPY . .

# バイナリをビルド
RUN go build -o server ./main.go

# 実行ステージ
FROM alpine:latest

WORKDIR /app

# テンプレートファイルをコピー
COPY --from=builder /app/templates ./templates

# ビルドしたバイナリをコピー
COPY --from=builder /app/server .

# ポートを公開
EXPOSE 8080

# サーバーを起動
CMD ["./server"]