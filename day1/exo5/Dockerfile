FROM golang:1.21.3 AS Builder
WORKDIR /go/src
COPY . .
RUN go get -d . && CGO_ENABLED=0 GOOS=linux go build -o /go/bin/helloworld .
# FROM scratch
# COPY --from=Builder /go/bin/helloworld /helloworld
CMD ["/go/bin/helloworld"]
