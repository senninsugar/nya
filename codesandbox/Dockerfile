# ベースイメージの指定
FROM python:3.11-slim

# コンテナ内の作業ディレクトリを設定
WORKDIR /app

# 環境変数の設定 (Pythonがpycファイルを作成しないようにし、標準入出力をバッファリングしない)
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# 依存関係のインストールに必要な最小限のツールをインストール（必要に応じて）
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# requirements.txt をコピーしてインストール
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# アプリケーションのソースコードをコピー
# (main.py と templates フォルダがカレントディレクトリにある想定)
COPY . .

# アプリケーションが使用するポートを公開
EXPOSE 8000

# アプリケーションを起動
# main:app は main.py の app インスタンスを指します
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
