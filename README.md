# Cloudsmith - Python Github Action

Interact with Cloudsmith repositories using the cloudmsith cli to push packages, etc. This action uses the Cloudsmith CLI and intends to be as similar to its structure and terminology as possible.  

## Cloudsmith API Key

The API key is required for the cloudsmith-cli to work.  

Obtain the API Key from [Cloudsmith user settings](https://cloudsmith.io/user/settings/api/). You should use a less priveleged and generic account for Continuous Integration.

Add a secret named `CLOUDSMITH_API_KEY` and a value of the API Key obtained from cloudsmith.  Secrets are maintained in the settings of each repository.

Pass your secret to the Action as seen in the Example usage.

## Python File Push - Example

[
![Package Workflow Status](https://github.com/apoclyps/python-github-action/workflows/Push%20Python/badge.svg)](https://github.com/apoclyps/python-github-action/actions?query=workflow%3A%22Push+Python%22)

[![Latest Version @ Cloudsmith](https://api-prd.cloudsmith.io/badges/version/apoclyps/testing-private/python/requests/latest/xf=sdist;xn=requests/?render=true&badge_token=gAAAAABeKMwXuMMxwGYNSZnobhHdAtOW9-twTlWw8yfcUUU1XVNmMFLNX3PdBPCKoiUOwYYPRrH76nMQLDY5APvg974YlniVCJOqg11XUq0Vwjbd9mGv-UQ%3D)](https://cloudsmith.io/~apoclyps/repos/testing-private/packages/detail/python/requests/latest/xf=sdist;xn=requests/)

See [push_python.yml](.github/workflows/push_python.yml)

```yml
name: Push Python
on: push
jobs:
  push:
    runs-on: ubuntu-latest
    name: Python File Push Test
    steps:
    - uses: actions/checkout@v1
    - name: Push
      id: push
      uses: apoclyps/python-github-action@master
      with:
        api-key: ${{ secrets.CLOUDSMITH_API_KEY }}
        command: 'push'
        format: 'python'
        owner: 'apoclyps'
        repo: 'testing-private'
        file: 'test/fixture/requests-2.22.0.tar.gz'
        republish: 'true' # needed since version is not changing
```
