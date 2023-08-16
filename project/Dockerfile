FROM python:3.9.6-alpine

# set work directory
WORKDIR /usr/src/project

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install psycopg2 dependencies
RUN apk update && apk add postgresql-dev gcc  python3-dev musl-dev

# install dependencies
RUN pip install --upgrade pip
RUN pip install gunicorn
#RUN apk update && apk add g++ gcc libxml2 libxslt-dev
COPY ./requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# copy entrypoint.sh
COPY ./entrypoint.sh /usr/src/project/entrypoint.sh
RUN sed -i 's/\r$//g' /usr/src/project/entrypoint.sh
RUN chmod +x /usr/src/project/entrypoint.sh

# copy project
COPY . .

# run entrypoint.sh
ENTRYPOINT ["/usr/src/project/entrypoint.sh"]



