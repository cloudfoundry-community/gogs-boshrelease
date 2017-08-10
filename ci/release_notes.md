## Changes

* Upgrade to gogs 0.11.19
* Added `bosh2 deploy manifests/gogs.yml` and updated README
* [Setup CI](https://ci.starkandwayne.com/teams/main/pipelines/gogs-boshrelease) to test pull requests
and master branch, and ship releases

In v5.0.0 the properties required for the jobs have not changed. In v6+ the job properties will be refactored, and bosh2 links will be used to link `gogs` to `postgres` job.
