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
bosh deploy manifests/gogs.yml
```

If your BOSH does not have Credhub/Config Server, then remember ` --vars-store` to allow generation of passwords and certificates:

```
bosh deploy manifests/gogs.yml --vars-store tmp/creds.yml
```

To register a route via your Cloud Foundry load balancer + router, you can use `manifests/operators/routing.yml`. If your Cloud Foundry deployment name is `cf`, and your system domain is `system.ourcompany.com`:

```
bosh deploy manifests/gogs.yml \
  -o manifests/operators/routing.yml \
  -v routing-nats-deployment=cf \
  -v gogs-uri=gogs.system.ourcompany.com
```

You could also dynamically look up your system domain:

```
cf_deployment=cf
system_domain=$(bosh -d $cf_deployment manifest | bosh int - --path /instance_groups/name=api/jobs/name=cloud_controller_ng/properties/system_domain)

bosh deploy manifests/gogs.yml \
   --vars-store tmp/creds.yml \
  -o manifests/operators/routing.yml \
  -v routing-nats-deployment=$cf_deployment \
  -v "gogs-uri=gogs.$system_domain"

open https://gogs.$system_domain/user/sign_up
```
