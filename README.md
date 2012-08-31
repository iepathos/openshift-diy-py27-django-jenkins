How to configure Openshift DIY
======================
I hope you have created a new Openshift DIY app by now. 

Login to the application host using SSH key mentioned in your application home:

* `ssh c8812345:123214@<app_name>-username.rhcloud.com`

Change into the application tmp directory:

* `cd $OPENSHIFT_TMP_DIR`

Download Python2.7 and extract:

* `wget http://python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2`
* `tar jxf Python-2.7.3.tar.bz2`

Build and install Python (takes several minutes)

* `cd Python-2.7.3`
* `./configure --prefix=$OPENSHIFT_RUNTIME_DIR`
* `make ; make install`

Export new Python path for later configuration (**you will need to run this if you logout, etc.**):

* `export PATH=$OPENSHIFT_RUNTIME_DIR/bin:$PATH`

Check that new Python is used (should be `Python 2.7.3`):

* `python -V`

Install setuptools and pip

* `cd $OPENSHIFT_TMP_DIR`
* `wget http://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz`
* `tar zxf setuptools-0.6c11.tar.gz`
* `cd setuptools-0.6c11`
* `python setup.py install`
* `cd $OPENSHIFT_TMP_DIR`
* `wget http://pypi.python.org/packages/source/p/pip/pip-1.1.tar.gz`
* `tar zxf pip-1.1.tar.gz`
* `cd pip-1.1`
* `python setup.py install`

Setup virtualenv:
* `cd $OPENSHIFT_DATA_DIR`
* `virtualenv $OPENSHIFT_APP_NAME --distribute`

Install uWSGI in it:
* `source $OPENSHIFT_DATA_DIR/$OPENSHIFT_APP_NAME/bin/activate`
* `pip install uwsgi` If this is not working, change to `cd $OPENSHIFT_TMP_DIR` and do.

Cleanup
* `cd ~`
* `rm -rf $OPENSHIFT_TMP_DIR/*`

Application Setup
===================

* Clone your initial DIY repo
* Download this project and add to it
* `git push origin master`

* Note
=======
If you change the Django application name (in the repo it's named `app`) you will also need to update the `.app_name` file with the new name in order for the OpenShift start/stop scripts to work.


* Contributors
==============
@ehazlett, @zemanel, Nam Duong (Red Hat)