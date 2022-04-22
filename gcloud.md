# Goggle Cloud Notes

### Gcloud auth
```
gcloud auth list
```

### Show gcloud config
```
gcloud config list
```

### Set project
```
gcloud config set project <name>
```

### Set region and zone
```
gcloud config set compute/region <region-name>
gcloud config set compute/zone <zone-name>

e.g.
gcloud config set compute/region us-central1
gcloud config set compute/zone us-central1-a
```

#### Show default region and zone
```
gcloud config get-value compute/region
gcloud config get-value compute/zone
```

- View list of regions and zones
```
gcloud compute regions list
gcloud compute zones list
```


## Create VM from public image
- https://cloud.google.com/compute/docs/instances/create-start-instance#gcloud
- https://bitbucket.org/wx_rds/decision-engine/src/master/docs/CONTRIBUTING.rst
- https://gcpinstances.doit-intl.com/?selected=n2-highmem-4

```
# Ensure current project is set to gcp-wow-rwds-ai-mmm-dev:
gcloud config set project gcp-wow-rwds-ai-mmm-dev

gcloud compute instances create jnguyen-dev-1 \
--project=gcp-wow-rwds-ai-mmm-dev \
--zone=us-central1-a \
--machine-type=n2-highmem-4 \
--network=mmm-dev-vpc \
--subnet=mmm-dev-usce1-subnet \
--no-address \
--image-family=ubuntu-2004-lts \
--image-project=ubuntu-os-cloud \
--boot-disk-size=200GB \
--boot-disk-type=pd-standard \
--metadata=enable-oslogin=TRUE

gcloud compute instances add-tags jnguyen-dev-1 \
--tags=iap-enabled
```

## Login
```
gcloud compute ssh jnguyen-dev-1 \
--zone us-central1-a \
--project gcp-wow-rwds-ai-mmm-dev \
--ssh-flag="-L 8081:localhost:8081" \
--tunnel-through-iap

# OR
gcloud compute ssh jnguyen-dev-1 \
--zone us-central1-a \
--project gcp-wow-rwds-ai-mmm-dev

# OR
gcloud compute ssh jnguyen11_woolworths_com_au@jnguyen-dev-1 \
--project gcp-wow-rwds-ai-mmm-dev \
--ssh-flag="-L 8080:localhost:8080"
```

## Debugging

### `gcloud auth login`: authentication link doesn't show up

Error message:
```
You are authorizing client libraries without access to a web browser. Please run the following command on a machine with a web browser and copy its output back here. Make sure the installed gcloud version is 372.0.0 or newer
```

[Solution](https://stackoverflow.com/questions/71561730/authorizing-client-libraries-without-access-to-a-web-browser-gcloud-auth-appli):
```
gcloud auth login --no-launch-browser
```

