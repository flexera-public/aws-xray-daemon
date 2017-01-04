This repository produces a Docker image that can be used to run the AWS X-Ray daemon inside a container.

**WARNING:** the daemon binds to `0.0.0.0` by default, which could present
a security hazard in some deployment scenarios. Do not publish the daemon's
exposed ports to the host unless you know what you are doing.

Limitations
-----------

This image is intended primarily for development-and-test scenarios; its
default configuration disables useful AWS-only features such as region
detection via EC2 metadata and IAM role assumption.

Usage
=====

To run with default configuration, provide the bare essential configuration
in the form of three environment variables:

```bash
docker run -e AWS_REGION=us-east-1 -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY xeger/aws-xray-daemon
```

To override the default configuration, map your own config file on
top of `/srv/cfg.yaml`:

```bash
docker run -v my-cfg.yaml:/srv/cfg.yaml xeger/aws-xray-daemon
```
