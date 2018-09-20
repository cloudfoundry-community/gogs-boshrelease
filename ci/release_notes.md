# Updates

The `routing.yml` operator file now introduces `bpm` into the VM for the upgraded `route_registrar` job.

It is likely that the `gogs` job will be upgraded to use `bpm` too soon.

Neither change should affect users.

# Versions

* gogs https://github.com/gogs/gogs to v0.11.66
* routing https://github.com/cloudfoundry/routing-release to v0.182.0
* introducing bpm v0.12.3 for routing-release