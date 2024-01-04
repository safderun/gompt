## 📬 GOMTP

Gomtp is a cli tool to test smtp settings easily.

## Install

### Install From Binary (Recommended)

You can install the `gomtp` to Linux or macOS with these commands:

```bash
sudo curl -L -o /usr/local/bin/gomtp "https://github.com/safderun/gomtp/releases/latest/download/gomtp-$(uname -s)-$(uname -m)" && \
sudo chmod +x /usr/local/bin/gomtp
```

### Build Locally

You can build the `gomtp` locally, on your own machine.

```bash
version=$(git describe --tags --abbrev=0) && \
commitId=$(git rev-parse --short $version) && \
go build -ldflags "-X gomtp/cmd.version=$version -X gomtp/cmd.commitId=$commitId" -o gomtp -v .
```

## Usage

- Create a `gomtp.yaml` file anywhre you want.
- Take the template from the `gomtp.yaml`
- There is 4 templates for `mailhog`, `gmail`, `yandex` and `brevo`
- `subject` and `body` is optional.
- In the same directory with your configured `gomtp.yaml`, run `gomtp` with no argument.

```bash
❯ gomtp
Email sent successfully!
```

- If your configuration is valid, you will see the "Email sent successfully!" message.

## Custom Gomtp Yaml Path

- You can name the `gomtp.yaml` as you wish while creating the configuration.

- If you change the default configuration file name, you can pass the path of the file to the `gomtp`.

```bash
gomtp --file test.yaml
```

or

```bash
gomtp -f test.yaml
```

## Sample SMTP For Testing

- To test the `gomtp` quickly, you can run the `mailhog` from `docker-compose.yml`

```bash
docker compose up -d
```

- Configure `gomtp.yaml`
  - The default `gomtp.yaml` file has been configured for the mailhog.
- Open the `mailhog` web ui from http://127.0.0.1:8025
- Run the `gomtp`.

```bash
gomtp
```

## Run Tests

- You can run e2e tests to ensure application stability.

```bash
go test -c -o gomtp.test ./cmd/ \
&& ./gomtp.test
```

- Check the test coverage:

```bash
go test -coverprofile=coverage.out -c -o gomtp.test ./cmd/ \
&& ./gomtp.test -test.coverprofile ./c.out | tee testCoverage.out
```

- You can see covered lines with html report:

```bash
go test -coverprofile=coverage.out -c -o gomtp.test ./cmd/ \
&& ./gomtp.test -test.coverprofile ./c.out \
&& go tool cover -html=c.out
```
