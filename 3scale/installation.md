# Guide

* Template based install: https://access.redhat.com/documentation/en-us/red_hat_3scale/2.2/html-single/infrastructure/#onpremises-installation

## Requirements

* An AWS account with an S3 bucket created within it.
* AWS access token and secret token (that has S3 read/write permissions).

## Install

Pull the `amp-s3.yml` template (we can't use the standard `amp.yml` because OSD doesn't allow RWX PVs). 

```bash
curl https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.2.0.GA/amp/amp-s3.yml > amp-s3.yml
```

Create the resources in the template, with the following parameters:

* `WILDCARD_DOMAIN` - The routing suffix of the cluster.
* `AWS_REGION` - The region of the AWS bucket (e.g. `us-east-1`).
* `AWS_BUCKET` - The name of the bucket to use in the `AWS_REGION`.
* `AWS_ACCESS_KEY_ID` - AWS Access Key
* `AWS_SECRET_ACCESS_KEY` - AWS Secret Access Key
* `FILE_UPLOAD_STORAGE` - This should always have the value `s3`.

For example.

```bash
oc new-app -f amp.yml --param WILDCARD_DOMAIN=192.168.0.73.nip.io AWS_REGION=us-east-1 AWS_BUCKET=my-bucket AWS_ACCESS_KEY_ID=XXXXXXXXX AWS_SECRET_ACCESS_KEY=XXXXXXXXX FILE_UPLOAD_STORAGE=s3
```

The output of the command will give you a login URL, username and password.
