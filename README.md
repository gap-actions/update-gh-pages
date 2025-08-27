# update-gh-pages

This GitHub action updates (or creates) the `gh-pages` branch of a GAP package using
[GitHubPagesForGAP](https://github.com/gap-system/GitHubPagesForGAP).

## Usage

The action `update-gh-pages` has to be called by the workflow of a GAP
package. By default, it will use the latest release of the package.

### Inputs

All of the following inputs are optional.

- `version`:
  - Set to a non-empty string to choose a specific release of your package (e.g. `v1.2.3`)
    instead of the latest release.
  - default: `''`
- `clean`:
  - Set to `false` to only update the information on the website and not the website code itself.
    This can be useful if you have made modifications to it.
  - default: `true`
- `dry-run`:
  - Set to `true` to create an archive containing the website instead of pushing to the `gh-pages` branch.
  - default: `false`

### Example

See below for a minimal example to run this action.

#### Minimal example
```yaml
name: Update GH-pages
on:
  workflow_dispatch:

permissions: write-all

jobs:
  update:
    name: Update GH pages
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - uses: gap-actions/setup-gap@v2
      - uses: gap-actions/update-gh-pages@v1
```

#### Example with inputs
```yaml
name: Update GH-pages
on:
  workflow_dispatch:
    inputs:
      version:
        description: 'Set to a non-empty string to choose a specific release of your package'
        required: false
        type: string
        default: ''
      clean:
        description: 'Set to false to only update the information on the website and not the website code itself'
        required: false
        type: boolean
        default: true
      dry-run:
        description: 'Set to true to create an archive containing the website instead of pushing to the gh-pages branch'
        required: false
        type: boolean
        default: false

permissions: write-all

jobs:
  update:
    name: Update GH pages
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - uses: gap-actions/setup-gap@v2
      - uses: gap-actions/update-gh-pages@v1
        with:
          version: ${{ inputs.version }}
          clean: ${{ inputs.clean }}
          dry-run: ${{ inputs.dry-run }}
```

## Contact
Please submit bug reports, suggestions for improvements and patches via
the [issue tracker](https://github.com/gap-actions/update-gh-pages/issues).

## License
The action `update-gh-pages` is free software; you can redistribute
and/or modify it under the terms of the GNU General Public License as published
by the Free Software Foundation; either version 2 of the License, or (at your
opinion) any later version. For details, see the file `LICENSE` distributed
with this action or the FSF's own site.
