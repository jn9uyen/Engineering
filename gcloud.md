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

### [Show bigtable instances](https://cloud.google.com/bigtable/docs/deleting-instance)
```
gcloud bigtable instances list
```
Delete instance:
- When you delete a Cloud Bigtable instance, you permanently delete the instance's clusters and all of the data in those clusters. Deleting an instance cannot be undone.
```
gcloud bigtable instances delete INSTANCE_ID
```

### Set up cbt (cloud big table) cli
```
gcloud components update
gcloud components install cbt
```

### [Write data to bigtable](https://cloud.google.com/bigtable/docs/create-instance-write-data-cbt-cli?_ga=2.151194681.-1685935609.1606081332)

In terminal:
```
echo project = gcp-wow-rwds-ai-dschapter-dev > ~/.cbtrc
echo instance = jnguyen-real-time-ch >> ~/.cbtrc

cbt createtable mytabe
cbt ls  # list tables

cbt createfamily mytable cf1  # add one column family cf1
cbt ls mytable

# Put the value test-value in the row r1, using the column family cf1 and the column qualifier c1
cbt set mytable r1 cf1:c1=test-value
cbt read mytable
```
> output
```
r1
  cf1:c1                                   @ 2022/04/22-02:34:29.036000
    "test-value"
```

#### Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this quickstart, delete the instance. Deleting the .cbtrc file leaves you ready to work on a different project.
```
cbt deletetable mytable
cbt delete instance jnguyen-real-time-ch
rm ~/.cbtrc
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
