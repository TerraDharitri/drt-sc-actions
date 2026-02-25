# Github Actions for smart contracts

A Github Action for smart contracts which:
- builds the wasm files
- runs denali-rs and denali-go tests
- does a clippy check
- provides a report containing details about the smart contracts

## Usage

### Standard build

See [contracts.yml](.github/workflows/contracts.yml)
This uses fixed versions of rust and vmtools.
Ignores `eei` checks which allows the contracts to use features which are not live on the numbat mainnet yet.

```yml
name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  contracts:
    name: Contracts
    uses: TerraDharitri/numbat-actions/.github/workflows/contracts.yml@v1
    with:
      rust-toolchain: nightly-2022-01-17
      vmtools-version: v1.4.43
      extra-build-args: --ignore-eei-checks
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

### Additional options

The drtpy version can be specified by providing:
```yml
pip-drtpy-args: drtpy==1.2.3
```
