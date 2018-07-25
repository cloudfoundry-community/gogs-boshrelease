# Deploy Gogs to BOSH

One of the fastest ways to get [gogs](http://gogs.io/) running on any infrastructure is to deploy this bosh release.

* [Concourse CI](https://ci.starkandwayne.com/teams/main/pipelines/gogs-boshrelease?groups=gogs-boshrelease)
* Pull requests will be automatically tested against a bosh-lite (see `testflight-pr` job)
* New versions of [gogs](http://gogs.io/) will be automatically added as the latest blob
* Discussions and CI notifications at [#gogs-boshrelease channel](https://cloudfoundry.slack.com/messages/C6PMMSW3T/) on https://slack.cloudfoundry.org

## Usage

To upload and deploy this BOSH release, run `bosh deploy manifests/gogs.yml` and include some optional operator files.

For example, if you are running [cfdev](https://github.com/cloudfoundry-incubator/cfdev) you can target it and deploy gogs:

```plain
cf dev start
source <(cf dev bosh env)

git clone https://github.com/cloudfoundry-community/gogs-boshrelease.git
bosh -d gogs deploy gogs-boshrelease/manifests/gogs.yml \
  -o gogs-boshrelease/manifests/operators/routing.yml \
  -v routing-nats-deployment=cf \
  -v gogs-uri=gogs.v3.pcfdev.io

open https://gogs.v3.pcfdev.io/user/sign_up
```
