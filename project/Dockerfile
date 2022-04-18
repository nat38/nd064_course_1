FROM python:3.8-slim-buster

# We copy just the requirements.txt first to leverage Docker cache
COPY ./techtrends/requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install -r requirements.txt

COPY ./techtrends /app

ENTRYPOINT [ "python" ]

CMD [ "app.py" ]