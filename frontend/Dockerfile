FROM python:3.9-slim
# FROM python:3.9
WORKDIR /app
# 先複製 requirements 以利用快取
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8501
# 假設使用 streamlit 或 flask 啟動，請依實作調整
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]