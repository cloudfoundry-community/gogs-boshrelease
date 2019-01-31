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
  -v gogs-uri=gogs.v3.pcfdev.io \
  --vars-store creds.yml

open https://gogs.v3.pcfdev.io/user/sign_up
```

Note: `--vars-store creds.yml` is not required if your BOSH environment is configured with Credhub.

## Post Deploy Errand
To create an admin user after deploying GOGS, run the following errand.

This was moved from the `gogs_ctl` script to this errand as it was never executed previously
```
bosh -d gogs run-errand gogs-admin
```

## Deploy with Authentication Backends
You can deploy gogs with alternative authentication backends.

The supported backend types are available [on the gogs website](https://gogs.io/docs/features/authentication) with examples for each [here](https://github.com/gogs/gogs/tree/f2ecfdc96a338815ffb2be898b3114031f0da48c/conf/auth.d).

You can modify the operators files with multiple backends for each type, and using the examples in the gogs repository, and the example operators in this repository you can see how to add them. You can also add multiple backends of the same type
```
bosh -d gogs deploy gogs-boshrelease/manifests/gogs.yml \
  -o gogs-boshrelease/manifests/operators/ldap_auth.yml \
  -v gogs-uri=gogs.v3.pcf.dev.io \
  --vars-store creds.yml
```
