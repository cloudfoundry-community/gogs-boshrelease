# Deploy Gogs to BOSH

One of the fastest ways to get [gogs](http://gogs.io/) running on any infrastructure is to deploy this bosh release.

## Usage

To use this bosh release, first upload it to your bosh:

```
git clone https://github.com/cloudfoundry-community/gogs-boshrelease.git
cd gogs-boshrelease
bosh2 deploy manifests/gogs.yml
```

If your BOSH does not have Credhub/Config Server, then remember ` --vars-store` to allow generation of passwords and certificates:

```
bosh2 deploy manifests/gogs.yml --vars-store tmp/creds.yml
```
