VERSION 0.6
FROM golang:1.17.8-alpine3.14
WORKDIR /go-example


deps:
	COPY go.mod go.sum ./
	RUN go mod download

	# Output these back in case go mod download changes them.
	SAVE ARTIFACT go.mod AS LOCAL go.mod
	SAVE ARTIFACT go.sum AS LOCAL go.sum

# This may be invoked from the command line as `earthly +build`.
build:
  FROM +deps

	# Copy and build code.
	COPY main.go .
	RUN go build -o build/go-example main.go
	SAVE ARTIFACT build/go-example /go-example AS LOCAL build/go-example

docker:
	COPY +build/go-example .
	ENTRYPOINT ["/go-example/go-example"]
	SAVE IMAGE go-example:latest
