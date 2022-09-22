RUN echo "Installing pthon full base image"
FROM nginx:latest as builder
WORKDIR /srcode
COPY ./test ./test
COPY ./srcode/* ./
RUN echo "Build"

FROM alpine:latest as unitest
WORKDIR /unitest
COPY --from=builder /srcode/test ./test
RUN echo "this is unitest" > ./test

FROM alpine:latest as security
WORKDIR /sonar
COPY --from=builder /srcode/* ./
COPY --from=unitest /unitest/test ./test
RUN echo "this is security" > ./test

FROM reportengine:1 as emailreports
WORKDIR /reports
COPY --from=sonarsecurity /sonar/test ./test

FROM alpine:latest as webapp
WORKDIR /code
COPY --from=builder /srcode/*.py ./
