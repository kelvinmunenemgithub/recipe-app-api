FROM python:3.7-alpine
MAINTAINER Kelvin Munene

ENV PYTHONUNBUFFERED 1
ENV PYTHONBUFFERED 1
ENV LANG C.UTF-8


ENV APP_HOME=/app
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

RUN apk update && \
    apk add --virtual build-deps gcc python3-dev musl-dev && \
    apk add postgresql-dev

RUN pip3 install --upgrade pip

COPY . $APP_HOME

COPY ./requirements.txt $APP_HOME/requirements.txt

RUN pip3 install -r requirements.txt

# create the app user
RUN addgroup -S app && adduser -S app -G app

# chown all the files to the app user
RUN chown -R app:app $APP_HOME

# change to the app user
USER app
