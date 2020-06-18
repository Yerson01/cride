FROM python:3
ENV PYTHONUNBUFFERED 1

RUN apk update \
    # pycopg2 dependencies
    && apk add --virtual build-deps gcc python3-dev musl-dev \
    && apk add postgresql-dev \
    # Pillow dependencies
    && apk add jpeg-dev z-lib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev \
    # CFFI dependencies
    && apk add libffi-dev py-cffi \
    # Translations dependencies
    && apk add gettext \
    && apk add postgresql-client

# Requirements are installed here to ensure they will be cached
COPY ./requirements /requirements
RUN pip install -r /requirements/local.txt


RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install - requirements.txt
COPY . /code/