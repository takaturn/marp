FROM mcr.microsoft.com/devcontainers/base:bookworm

# marpでpptxファイル変換するために必要なパッケージをインストール
# * ブラウザ・・・Firefox
# * 日本語フォント・・・明朝体系のやつ
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        firefox-esr=* \
        fonts-takao-mincho=* \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
