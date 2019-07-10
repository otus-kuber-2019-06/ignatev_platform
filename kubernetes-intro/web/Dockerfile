FROM golang:alpine AS build
RUN apk update && apk add --no-cache git
RUN go get -u github.com/m3ng9i/ran
WORKDIR /go/src/github.com/m3ng9i/ran
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build
RUN adduser --disabled-password -u 1001 www

FROM scratch
COPY --from=build /go/src/github.com/m3ng9i/ran/ran /ran
COPY --from=build /etc/passwd /etc/passwd
COPY homework.html /app/homework.html
EXPOSE 8000
USER 1001
CMD ["/ran", "-p", "8000", "-r", "/app"]
