FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 8080
USER 1000
RUN sleep 300
CMD [ "python","app.py" ]

