FROM python:3.7-alpine
MAINTAINER Kelvin Munene

ENV PYTHONUNBUFFERED 1
ENV PYTHONBUFFERED 1
ENV LANG C.UTF-8

COPY ./requirements.txt /requirements.txt
RUN apk add --update --no-cache postgresql-client jpeg-dev
RUN apk add --update --no-cache --virtual .tmp-build-deps \
    gcc libc-dev linux-headers postgresql-dev musl-dev zlib zlib-dev
RUN pip3 install -r /requirements.txt
RUN apk del .tmp-build-deps

RUN mkdir /app
WORKDIR /app
COPY ./app /app

RUN mkdir -p /vol/web/media
RUN mkdir -p /vol/web/static
RUN adduser -D user
RUN chown -R user:user /vol/
RUN chown -R 755 /vol/web
USER user


#ENV APP_HOME=/app
#RUN mkdir $APP_HOME
#WORKDIR $APP_HOME
#
#RUN apk update && \
#    apk add --virtual build-deps gcc python3-dev musl-dev && \
#    apk add postgresql-dev
#
#RUN pip3 install --upgrade pip
#
#COPY . $APP_HOME
#
#COPY ./requirements.txt $APP_HOME/requirements.txt
#
#RUN pip3 install -r requirements.txt
#
## create the app user
#RUN addgroup -S app && adduser -S app -G app
#
## chown all the files to the app user
#RUN chown -R app:app $APP_HOME
#
## change to the app user
#USER app
