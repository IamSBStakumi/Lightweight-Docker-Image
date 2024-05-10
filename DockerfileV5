FROM python:3.11.9-slim-bullseye as builder

# 必要なパッケージ
RUN apt-get update -q
RUN apt-get -y upgrade --no-install-recommends
RUN apt-get -y install libopencv-dev

# pipのアップグレードとpoetryのインストール
RUN pip install --upgrade pip && \
    pip install poetry && \
    # 仮想環境を作らないよう設定
    poetry config virtualenvs.create false

FROM python:3.11.9-slim-bullseye as dev
# タイムゾーンを日本に設定
ENV TZ Asia/Tokyo

COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin

WORKDIR /workspace/app

EXPOSE 8888
