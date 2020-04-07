FROM python:3.6

ADD . /code
WORKDIR /code

COPY scrapyd.conf /etc/scrapyd/

EXPOSE 6800

RUN pip install -r requirements
CMD scrapyd
