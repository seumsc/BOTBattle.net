FROM ubuntu:18.04
COPY sources.list /etc/apt/

ARG KEY=default_key

RUN apt-get update \
    && apt-get install -y python python-pip git vim

RUN pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple Django==2.1 \
    && pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple requests

RUN cd /root \
    && git clone --single-branch -b master https://github.com/Botbattle-net/BOTBattle.net \
    && touch /root/BOTBattle.net/secretkey.py \
    && echo "secretKey = '$KEY'" >> /root/BOTBattle.net/secretkey.py \
    && mkdir /root/BOTBattle.net/log \
    && cd /root/BOTBattle.net \
    && python manage.py migrate --run-syncdb #cache

CMD cd /root/BOTBattle.net \
    && python manage.py runserver 0.0.0.0:8001 >> runserver.log