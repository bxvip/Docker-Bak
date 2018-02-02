# http://blog.csdn.net/yhcvb/article/details/45696961
FROM python:2.7
ENV PYTHONWNBUFFERED 1
RUN mkdir /code
RUN MKDIR /code/db
WORKDIR /code
ADD ./mysite/requirements.txt /code/
RUN pip install -r requirements.txt
Add ./code/