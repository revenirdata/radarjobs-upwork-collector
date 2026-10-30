# RadarJobs Upwork Collector

This public scheduler runs RadarJobs' native, signed-out Upwork marketplace collector on a standard GitHub-hosted runner every 30 minutes. It submits the acquired manifest to the authoritative Radar Processing service.

## Cost and access boundaries

- The scheduled workflow uses a public-repository GitHub-hosted runner, so GitHub Actions minutes are not billed.
- It does not use Bright Data, another paid proxy, a local computer, or email forwarding.
- RadarJobs authenticates the workflow with a short-lived GitHub OIDC token scoped to this repository, workflow, branch, and event type.
- A read-only deploy key checks out the exact private backend revision reported by production. The collector cannot push backend changes.

The workflow deliberately runs at `17` and `47` minutes past each hour to avoid the top-of-hour scheduler surge.
