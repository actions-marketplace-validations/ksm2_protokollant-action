protokollant
============

Perform platform-agnostic releases using [Protokollant].

Protokollant performs releases of your application and maintains the changelog.

For more information about supported languages, [read the docs][Protokollant].


## Usage

See [action.yml](action.yml)

### To perform a major version bump

```yaml
uses: ksm2/protokollant-action@v1
with:
  bump: major
```

### To perform a prerelease

```yaml
uses: ksm2/protokollant-action@v1
with:
  bump: prerelease
  unreleased: true
  changelog: false
```

### Using a specific version of Protokollant

```yaml
uses: ksm2/protokollant-action@v1
with:
  bump: prerelease
  protokollant-version: 0.5.0
```

### Using a manual workflow

```yaml
on:
  workflow_dispatch:
    inputs:
      bump:
        description: "The version bump to perform"
        required: true
        type: choice
        default: patch
        options:
          - patch
          - minor
          - major
            
jobs:
  bump:
    steps:
      - uses: actions/checkout@v3
      - uses: ksm2/protokollant-action@v1
        with:
          bump: ${{ inputs.bump }}
```


## Inputs

### `bump`

**Required** The bump to perform on the repository, should be one of

- `"major"`
- `"minor"`
- `"patch"`
- `"prerelease"`

### `diff`

If `true`, will only print the diff. Default `false`.

### `unreleased`

If `true`, will prepend an unreleased section before bumping. Default `false`.

### `changelog`

If `false`, will skip writing to the changelog. Default `true`.

### `protokollant-version`

The version of [Protokollant] to use, defaults to `"latest"`.


## Outputs

### `version`

The new version of the application.

### `previous-version`

The former version of the application.

### `bump`

Returns `true` if the version was bumped.

### `protokollant-version`

The version of [Protokollant] being used.

### `protokollant-path`

The absolute path to which [Protokollant] was installed.


[Protokollant]: https://github.com/ksm2/protokollant
