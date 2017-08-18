# Deploy Gogs to BOSH

One of the fastest ways to get [gogs](http://gogs.io/) running on any infrastructure is to deploy this bosh release.

* [Concourse CI](https://ci.starkandwayne.com/teams/main/pipelines/gogs-boshrelease?groups=gogs-boshrelease)
* Pull requests will be automatically tested against a bosh-lite (see `testflight-pr` job)
* New versions of [gogs](http://gogs.io/) will be automatically added as the latest blob
* Discussions and CI notifications at [#gogs-boshrelease channel](https://cloudfoundry.slack.com/messages/C6PMMSW3T/) on https://slack.cloudfoundry.org

## Usage

To use this bosh release, first upload it to your bosh:

```
export BOSH_ENVIRONMENT=<alias>
export BOSH_DEPLOYMENT=gogs

git clone https://github.com/cloudfoundry-community/gogs-boshrelease.git
cd gogs-boshrelease
bosh2 deploy manifests/gogs.yml
```

If your BOSH does not have Credhub/Config Server, then remember ` --vars-store` to allow generation of passwords and certificates:

```
bosh2 deploy manifests/gogs.yml --vars-store tmp/creds.yml
```
