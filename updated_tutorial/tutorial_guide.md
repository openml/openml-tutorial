# OpenML Python API Tutorial (Sept 2026)
_Laith Agbaria and the OpenML Team_

> “OpenML is an online platform for open science collaboration in machine learning, used to share datasets and results of machine learning experiments.”  
> — [Feurer et al. (2021)](https://jmlr.org/papers/volume22/19-920/19-920.pdf)

This tutorial is intended to introduce you to the [OpenML](https://www.openml.org/) Python API, giving you detailed examples of how to use various functionalities necessary to utilize the existing tools.
There are two jupyter notebooks associated with this tutorial that first show the various functions through examples and then provide guided exercises to develop skills, we hope that you use the test (or a [docker local](https://github.com/openml/services)) server throughout the tutorial so as not to populate the main website with tutorial examples.
If you encounter any issues during this tutorial or have any recommendations after completing it, contact us through the [official Slack channel](https://openml.slack.com), your experience matters to us and those who will start with the tutorial later on.

There is currently no advanced usage tutorial, however a detailed [documentation](https://openml.github.io/openml-python/latest) should offer answers to most queries, you could also contact us through the [official Slack channel](https://openml.slack.com) or in one of the [hackathons](https://openml.org/meet).

### Prerequisites
To follow this tutorial, you will need:
- Python 3.10+ for the most recent OpenML versions,
- Jupyter notebook (can run in Google Colab),
- Pip or Anaconda package environment,
- OpenML account.

### OpenMLBase
The OpenMLBase class exists at the core of the API, it is a parent class for datasets, tasks, flows, runs, and studies. Through this base class, OpenML objects can have an ID and URL, publish then push/remove tags, and open the default web browser directly to the calling object page.

### Test server
There exists a test version of the OpenML server intended for learning how the API functions, using it should appear identical to using the main server but without adding any clutter. We would advice and appreciate the use of this server for any uploads during the learning process.
```python
import openml
openml.config.start_using_configuration_for_example()
# ...
openml.config.stop_using_configuration_for_example()
```

## Datasets
OpenML datasets are standardized and hosted on the OpenML platform, and each dataset contains the data itself together with metadata describing its structure and intended use. This metadata can include the dataset name, identifier, number and types of features, target variable, number of instances, and information about missing values. OpenML uses this standardized representation to make datasets easy to discover, share, download, and use consistently across machine-learning experiments.

Shown in the examples notebook is the listing of datasets using the function ```openml.dataset.list_datasets()```, by default this function returns a Python dictionary, however this is planned to change in later versions into a pandas DataFrame. This could already be achieved by using the parameter ```output_format='dataframe'```.

When using ```openml.datasets.get_dataset()``` to load a dataset, it creates a cache in the directory ```openml.config.get_cache_directory()```. Setting the parameter ```download_data=True``` will result in an attempt to download a Paraquet version if it exists, if no version exists then it will fall back to downloading the ARFF version. Setting the ```OPENML_SKIP_PARAQUET_ENV_VAR``` to ```true``` in the OpenML package environment would lead to the same result.

OpenML datasets typically come with a ```default_target_attribute```, which can be used to directly separate the target data from the features data when using ```get_data(target)```.  By default this function already returns a pandas DataFrames, and has four outputs (features, target, categorical indicator, attribute names).

The metadata could be accessed through the dataset object directly and it contains authors, descriptions, tags, and more,or through ```dataset.details``` when loading through ```sklearn.datasets.fetch_openml()```.

An API key is mandatory to publish anything, including datasets, to OpenML, and a created dataset requires publication to be usable with the OpenML framework. You are able to fork a version of any published dataset, and then edit any dataset you own, do note that datasets currently used by tasks can only be modified in specific ways.
If you would like to delete a dataset you own, then you must first detach it from all tasks.

## Tasks

## Runs and flows

## Studies

# References
- Feurer, M., van Rijn, J. N., Kadra, A., Gijsbers, P., Mallik, N., Ravi, S., Müller, A., Vanschoren, J., & Hutter, F. (2021). OpenML-Python: An extensible Python API for OpenML. Journal of Machine Learning Research, 22, 1–5. https://jmlr.org/papers/volume22/19-920/19-920.pdf
