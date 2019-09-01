## Create a lambda layer with matplotlib (and netCDF4 and requests)
Additionally adds netCDF4 and requests library.

Adapted from the best bits of two helpful pages:

https://nordcloud.com/lambda-layers-for-python-runtime/#LambdalayersforPythonruntime-CreateYourownlayer!

https://medium.com/@manivannan_data/import-custom-python-packages-on-aws-lambda-function-5fbac36b40f8

### Requirements
Python 3.7 (or whatever version you are using in your AWS Lambda function)

### Building the layer package
We will create a new virtualenv, taking care to use the right python version for all commands, and use the resulting
lib folder for our layer package. I dont know whether leaving out lib64 has any real consequences.

```
python3.7 -m venv python
source python/bin/activate
python3.7 -m pip install matplotlib netCDF4 requests
deactivate
```

As of writing, this installs these packages:
```
certifi-2019.6.16 cftime-1.0.3.4 chardet-3.0.4 cycler-0.10.0 idna-2.8 kiwisolver-1.1.0 matplotlib-3.1.1 netCDF4-1.5.1.2 numpy-1.17.1 pyparsing-2.4.2 python-dateutil-2.8.0 requests-2.22.0 six-1.12.0 urllib3-1.25.3
```

Create a layer zip containing these packages, seems AWS is happy just being provided with the lib folder only.
```
zip -r awslambda-matplotlib-layer.zip python/lib
```
Upload zip to AWS, apply newly created layer to your lambda function.
