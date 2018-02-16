# jupyter_setup on MacOS

1. Install Anaconda Navigator by going to this site https://www.anaconda.com/download/#macos
Choose Python 2.7 version.

2. After installing Anaconda Navigator, it should have automatically generated a PATH line on your ~/.bash_profile. 
It should be something similar below. You will have to make sure that this should come first on your PATH so that when Jupyter runs
it will use the python package that came with Anaconda as oppose to the default python package from MacOS.
```
# added by Anaconda2 5.0.1 installer
export PATH="/Users/rgarcia/anaconda2/bin:$PATH"
```
Make sure to re-load the latest changes by running the command below.
```
source ~/.bash_profile
```
Check to see if you are now using the Anaconda Python 
```
which python
```

3. You cannot load data into Kinetica if you are using pandas-datareader (0.6.0). Use an older version which is 0.5.0. Go to the
site below and download it and put it to your local filesystem. 

https://pypi.python.org/packages/9b/3b/5fae1f4ba5889468fefbadcefda0389f60f2780eead3a1166415bda4509c/pandas-datareader-0.5.0.tar.gz#md5=77cc22b08b5cac46eb974ac6687d4555

4. Go to the directory where you downloaded the pandas-datareader and unzip it. 
5. Change directory to the unzipped folder and list directory. You should see something simlar below.
```
Rommels-MBP-2:~ rgarcia$ ls -la ~/Documents/Training/UDF/pandas-datareader-0.5.0
total 48
drwxr-xr-x@ 12 rgarcia  staff   384 Feb 13 16:26 .
drwxr-xr-x@ 16 rgarcia  staff   512 Feb 13 17:10 ..
-rw-r--r--@  1 rgarcia  staff  3769 Nov 16  2016 LICENSE.md
-rw-r--r--@  1 rgarcia  staff   145 Nov 16  2016 MANIFEST.in
-rw-r--r--@  1 rgarcia  staff  3487 Jul 25  2017 PKG-INFO
-rw-r--r--@  1 rgarcia  staff  2028 May 16  2017 README.rst
drwxr-xr-x   4 root     staff   128 Feb 13 16:26 build
drwxr-xr-x   3 root     staff    96 Feb 13 16:26 dist
drwxr-xr-x@ 22 rgarcia  staff   704 Jul 25  2017 pandas_datareader
drwxr-xr-x@  8 rgarcia  staff   256 Jul 25  2017 pandas_datareader.egg-info
-rw-r--r--@  1 rgarcia  staff    67 Jul 25  2017 setup.cfg
-rw-r--r--@  1 rgarcia  staff  1800 Jul 25  2017 setup.py
```

6. Install pandas-reader.
```
sudo python setup.py install
```

7. To check if pandas-reader was successfully installed, run the command below.
```
pip list | grep pandas
```

The output should be something similar below. If uout pandas version is newer, its ok. But you need to maske sure that the pandas-datareader is the exact same version. Ignore the warning for now.
```
Rommels-MBP-2:~ rgarcia$ pip list | grep pandas
DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
pandas (0.20.3)
pandas-datareader (0.5.0)
```

8. It is critical that you use the same Kinetica API Client version as the Kinetica server. You can grab the Python Kinetica API client
library below for 6.1.0. Since the Kinetica server we are connecting is on 6.1.0, we should download the client API with the same version.

https://github.com/kineticadb/kinetica-api-python/tree/release/v6.1.0

9. Download the zip Python API then unzip.

10. Update ~/.bash_profile and add to your path the api bin folder. Output should be similar below. 
```
export PATH=/Users/rgarcia/anaconda2/bin:/Users/rgarcia/Documents/Training/UDF/kinetica-api-python-release-v6.1.0/gpudb:$PATH
```

11. Change directory to the Python API client folder and set it up.
```
cd /Users/rgarcia/Documents/Training/UDF/kinetica-api-python-release-v6.1.0
sudo python setup.py install
```
Continue finishing the install and also install avro.
```
sudo pip install .
sudo pip install avro
```

Make sure to reload your changes.
```
source ~/.bash_profile
```

12. We will also need KiSQL. So make sure you have installed git on your host. Run the install. Make changes to the command to use your own account and the correct repo.
```
git clone https://your_user)_name@bitbucket.org/repo/kisql.git
```

13. Change directory into kisql then build kisql.
```
mvn clean package
```

14. A jar file should have been created under target folder. Run the command below.
```
cp kisql-1.0-SNAPSHOT-jar-with-dependencies.jar kisql /usr/local/bin/
```

15. Update ~/.bash_profile to include Kinetica parameters for KiSQL.
```
export KI_HOST="xxx.xxx.xxx.xxx"
KI_USER="username"
KI_PWD="password"
```
Now you can run kisql anywhere in your CLI. 
To know all avaiable kisql command options, run the command below.
```
kisql -help
```

Now you can open Anaconda Navigator and launch Jupyter.




