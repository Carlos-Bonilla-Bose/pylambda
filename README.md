# pylambda

## Objective

This is a ramda inspired (as opposed to ramda-like) set of tools for making my work with python a bit easier and enjoyable.

## Deployment

Nexus is being used as the artifacts manager, as such 2 steps are required

1. Using pip w/ nexus
2. Uploading packages to Nexus

### Using pip w/ nexus

The easiest way to use nexus is to add a parameter to the `requirements.txt` file.

```
--extra-index-url https://platform.bose.io/dev/svc-core-devops-nexus/prod/core-devops-nexus-core/repository/pypi-all/simple
dptools==1.0.1
```
Notice the url path ends with `simple`, this is a requirement of `pip`, which nexus makes available by default.

This parameter makes it such that the PyPI index is still part of the path, and if the package is not found there, then the "extra-index" is used. (not 100% sure about this order)

Alternatively, to limit pip to a specific index the flag `--index-url` can be used instead. Both flags can co-exist such that `--extra-index-url` augments the contents of `--index-url`.

### Uploading package to Nexus

The upload command needs an index, otherwise it will default to PyPI. The upload function defined in this repository uses the name `nexus` as the index. Consequently this index will need to be defined in `~/.pypirc`.

```
[distutils]
index-servers =
   nexus

[nexus]
repository = https://ingress-platform.live-aws-useast1.bose.io/dev/svc-core-devops-nexus/prod/core-devops-nexus-core/repository/dp-pytools/
username = #############
password = -------------
```

The upload process makes use of twine, to install just run the requirements.txt.

`pip install -r requirements.txt`

Once the configuration is set, and twine has been installed, simply upload to nexus:

`python setup.py upload`