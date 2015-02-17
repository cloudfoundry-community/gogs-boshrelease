# BOSH Release for gogs
One of the fastest ways to get [gogs](http://gogs.io/) running on any infrastructure is to deploy this bosh release.

## Usage

To use this bosh release, first upload it to your bosh:

```
bosh target BOSH_HOST
git clone https://github.com/cloudfoundry-community/gogs-boshrelease.git
cd gogs-boshrelease
bosh upload release releases/gogs-1.yml
```

For [bosh-lite](https://github.com/cloudfoundry/bosh-lite), you can quickly create a deployment manifest & deploy a cluster:

```
templates/make_manifest warden
bosh -n deploy
```
