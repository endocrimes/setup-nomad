# GitHub Action: setup-nomad

The `endocrimes/setup-nomad` Action sets up the `nomad` CLI in your GitHub Actions workflow by adding the binary to `PATH`.

## Usage

1.) Create GitHub Actions Secrets

- Set the `NOMAD_ADDR` to the IP-address or hostname of a Nomad cluster that is routable for GitHub Actions Runners.
- Set the `NOMAD_TOKEN` to a token with appropriate permissions to carry out action-specific operations on a Nomad cluster.

> **Warning**
> Running services such as Nomad on a publicly accessible port without authentication is a terrible idea.


2.) Create a GitHub Actions Workflow file (e.g.: `.github/workflows/nomad.yml`):

```yaml
name: nomad

on:
  - push

jobs:
  nomad:
    runs-on: ubuntu-latest
    name: Run Nomad
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup `nomad-pack`
        uses: endocrimes/setup-nomad@main
        id: setup
        with:
          version: "1.4.0" # or `latest`

      - name: Run `nomad status`
        id: info
        run: "nomad status"
```

## Inputs

This section contains a list of all inputs that may be set for this Action.

- `version` - (required) The version of `nomad` to install. Supports [semver](https://www.npmjs.com/package/semver) versioning. Defaults to `latest`.

## Outputs

This section contains a list of all outputs that can be consumed from this Action.

- `version` -  The version of `nomad` that was installed.

## Author Information

The original code of this repository is based on work done by [Matthew Sanabria](https://github.com/sudomateo) as part of the [setup-packer](https://github.com/sudomateo/setup-packer) GitHub Action and the contributors of the [setup-nomad-pack](https://github.com/hashicorp/setup-nomad-pack) action.

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.
