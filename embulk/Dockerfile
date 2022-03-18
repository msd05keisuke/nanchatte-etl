FROM openjdk:8-slim

ENV LANG=C.UTF-8 \
    PATH_TO_EMBULK=/opt/embulk \
    PATH=${PATH}:/opt/embulk

# タイムゾーンを変更
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# vim, ping などをインストール
RUN apt-get update && apt-get install -y curl vim
RUN apt-get install -y iputils-ping

# Embulk をインストール
RUN mkdir -p ${PATH_TO_EMBULK} \
    && curl --create-dirs -o ${PATH_TO_EMBULK}/embulk -L "https://dl.embulk.org/embulk-0.9.23.jar" \
    && chmod +x ${PATH_TO_EMBULK}/embulk

# mysql用のプラグインをインストール
RUN embulk gem install embulk-input-mysql 
RUN embulk gem install embulk-output-mysql
# filter用プラグインをインストール
# RUN embulk gem install embulk-filter-eval
RUN embulk gem install embulk-filter-column

# コンテナ側にconfig.ymlをコピー
WORKDIR /app
COPY ./config.yml ./

CMD [ "bash" ]