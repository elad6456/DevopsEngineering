RUN echo "Installing PYTHON LIBS"
WORKDIR /srcode
COPY ./test ./test
COPY ./srcode/* ./
RUN echo "BUILDING APP"

FROM alpine:latest as unitest
WORKDIR /unitest
COPY --from=builder /srcode/test ./test
RUN echo "IM RUNNING THE UNITEST" > ./test

FROM alpine:latest as security
WORKDIR /sonar
COPY --from=builder /srcode/* ./
COPY --from=unitest /unitest/test ./test
RUN echo "IM RUNNING THE SECURITY" > ./test

FROM reportengine:1 as emailreports
WORKDIR /reports
COPY --from=sonarsecurity /sonar/test ./test

FROM alpine:latest as webapp
WORKDIR /code
COPY --from=builder /srcode/*.py ./
