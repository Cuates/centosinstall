[How To Install Python 38 On CentOS 8](https://linuxize.com/post/how-to-install-python-3-8-on-centos-8/)<br />
[How To Install Python On 3 On CentOS](https://computingforgeeks.com/how-to-install-python-on-3-on-centos/)<br />
[Unable To Install Pyodbc On Linux](https://stackoverflow.com/questions/2960339/unable-to-install-pyodbc-on-linux)
* `sudo dnf groupinstall -y 'development tools'`
* `sudo dnf install -y bzip2 bzip2-devel expat-devel gdbm-devel ncurses-devel openssl-devel readline-devel wget sqlite-devel tk-devel xz-devel zlib-devel libffi-devel`
* `wget https://www.python.org/ftp/python/3.9.0/Python-3.9.0.tgz`
* `tar -xf Python-3.9.0.tgz`
* `cd Python-3.9.0`
* `./configure --enable-optimizations`
  * **WAIT FOR THIS TO FINISH**
* `nproc` (Displays the number of cores in your processor)
* `make -j 4`
  * **WAIT FOR THIS TO FINISH**
* `sudo make altinstall`
  * **WAIT FOR THIS TO FINISH**
  * **DO NOT `sudo make install` AS IT WILL OVERWRITE THE DEFAULT SYSTEM PYTHON**
* `sudo dnf install -y python3-devel` **THIS IS NEEDED FOR SOME OF THE PYTHON MODULES**
* `python3.9 --version`
* `pip3.9 --version`
* Upgrade pip version
  * `/usr/local/bin/python3.9 -m pip install --upgrade pip`
* Installing modules for Python
  * [Pandas](https://pypi.org/project/pandas/)
    * `pip3.9 install pandas`
      * **WAIT FOR THIS TO FINISH**
  * [SQLAlchemy](https://pypi.org/project/SQLAlchemy/)
    * `pip3.9 install sqlalchemy`
  * [psycopg2](https://pypi.org/project/psycopg2/)
    * `pip3.9 install psycopg2-binary`
  * **need to perform the following first before pyodbc and mysqlclient can be installed**
  * [Install dependencies for python3 and mysql](https://stackoverflow.com/questions/21530577/fatal-error-python-h-no-such-file-or-directory)
  * `sudo dnf install -y python3-devel mysql-devel unixODBC-devel` **IMPORTANT NOTE Install MariaDB first then do this command**
    * [pyodbc](https://pypi.org/project/pyodbc/)
      * `pip3.9 install pyodbc`
    * [mysqlclient](https://pypi.org/project/mysqlclient/)
      * `pip3.9 install mysqlclient`
        * If "NameError: name '\_mysql' is not defined", then proceed with the following instead
          * `pip3.9 uninstall mysqlclient`
          * `pip3.9 install --no-binary mysqlclient mysqlclient`
            * Note: The first occurrence is the name of the package to apply the no-binary option to, the second specifies the package to install
