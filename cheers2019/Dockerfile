FROM golang:1.11-alpine AS builder
RUN apk add --no-cache git
RUN cd /go/src && mkdir golang.org && cd golang.org && mkdir x && cd x && git clone https://github.com/golang/text.git text
RUN go get github.com/pdevine/go-asciisprite
WORKDIR /project
COPY cheers.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -ldflags '-extldflags "-static"' -o cheers cheers.go

FROM scratch
COPY --from=builder /project/cheers /cheers
ENTRYPOINT ["/cheers"]
