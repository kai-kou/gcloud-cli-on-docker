# gcloud-cli-on-docker


## Usage

```console
# credentials.dbなどがある前提
> ls ~/.config/gcloud/
access_tokens.db   config_sentinel    credentials.db     legacy_credentials
active_config      configurations     gce                logs


> docker-gcloud --version
Google Cloud SDK 267.0.0
bq 2.0.49
core 2019.10.15
gsutil 4.44


> cat <<EOF > cloudbuild.yaml
steps:
- name: 'gcr.io/cloud-builders/git'
  entrypoint: 'bash'
  args: ['-c', 'echo "hoge"']
EOF


> docker-gcloud builds submit \
  --config=cloudbuild.yaml \
  --no-source
Created [https://cloudbuild.googleapis.com/v1/projects/<GCPのProjectID>/builds/16cab9fd-a4b3-4937-a7a3-7838516788d3].
Logs are available at [https://console.cloud.google.com/gcr/builds/16cab9fd-a4b3-4937-a7a3-7838516788d3?project=168605712006].
---------------------------------------------------- REMOTE BUILD OUTPUT ----------------------------------------------------
starting build "16cab9fd-a4b3-4937-a7a3-7838516788d3"

FETCHSOURCE
BUILD
Already have image (with digest): gcr.io/cloud-builders/git
hoge
PUSH
DONE
-----------------------------------------------------------------------------------------------------------------------------

ID                                    CREATE_TIME                DURATION  SOURCE  IMAGES  STATUS
16cab9fd-a4b3-4937-a7a3-7838516788d3  2019-10-20T02:23:44+00:00  3S        -       -       SUCCESS


> docker-gcloud builds log \
  16cab9fd-a4b3-4937-a7a3-7838516788d3
---------------------------------------------------- REMOTE BUILD OUTPUT ----------------------------------------------------
starting build "16cab9fd-a4b3-4937-a7a3-7838516788d3"

FETCHSOURCE
BUILD
Already have image (with digest): gcr.io/cloud-builders/git
hoge
PUSH
DONE
-----------------------------------------------------------------------------------------------------------------------------
```

## Install

```console
> chmod +x docker-*
> ln -s docker-gcloud /usr/local/bin/
> ln -s docker-gsutil /usr/local/bin/
```
