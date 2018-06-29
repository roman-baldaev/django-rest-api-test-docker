FROM python:3.6
ENV PYTHONUNDUFFERED 1
ADD requirements.txt ./
RUN pip install -r /requirements.txt
RUN mkdir /src
WORKDIR /src
