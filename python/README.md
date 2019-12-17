FROM registry.cn-hangzhou.aliyuncs.com/last911/openresty-python3.7 AS build-env

ADD . /app
WORKDIR /app
COPY ./requirements.txt /app/requirements.txt
RUN pip3.5 install -r ./requirements.txt
COPY ./hello.py /app/hello.py

FROM try520/distroless_python3:latest
COPY --from=build-env /usr/local/lib/python3.5/dist-packages /usr/local/lib/python3.5/dist-packages
COPY --from=build-env /app /app
WORKDIR /app
CMD ["hello.py"]
