# 使用 golang alpine 作為編譯環境
FROM golang:1.21-alpine AS builder

# 安裝編譯 SQLite 必要的工具 (這行是解決 exit code 1 的關鍵)
RUN apk add --no-cache gcc musl-dev sqlite-dev

# 設定工作目錄
WORKDIR /app

# 複製設定檔並下載套件
COPY go.mod ./
# 如果你有 go.sum 請取消下一行註解
# COPY go.sum ./ 
RUN go mod download

# 複製程式碼
COPY . .

# 執行編譯 (加上 CGO_ENABLED=1 確保 SQLite 驅動能正常編譯)
RUN CGO_ENABLED=1 GOOS=linux go build -o main .

# 第二階段：極簡執行環境
FROM alpine:latest
WORKDIR /app

# 安裝執行時需要的函式庫
RUN apk add --no-cache libc6-compat libgcc libstdc++

# 從編譯階段複製執行檔
COPY --from=builder /app/main .

# 開放埠號
EXPOSE 8002

# 啟動
CMD ["./main"]