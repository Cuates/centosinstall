[How To Install Python 38 On CentOS 8](https://linuxize.com/post/how-to-install-python-3-8-on-centos-8/)<br />
[How To Install Python On 3 On CentOS](https://computingforgeeks.com/how-to-install-python-on-3-on-centos/)<br />
[Unable To Install Pyodbc On Linux](https://stackoverflow.com/questions/2960339/unable-to-install-pyodbc-on-linux)<br />
[Database_Drivers](https://crateanon.readthedocs.io/en/latest/installation/database_drivers.html)<br />
[Pythons mysqldb Cant Find libmysqlclient dylib With Homebrewed MySQL](https://stackoverflow.com/questions/34536914/pythons-mysqldb-can-t-find-libmysqlclient-dylib-with-homebrewed-mysql)
* `sudo dnf groupinstall -y 'development tools'`
* Version 8
  * `sudo dnf install -y bzip2 bzip2-devel expat-devel ncurses-devel openssl-devel readline-devel wget sqlite-devel tk-devel xz-devel zlib-devel libffi-devel gdbm-devel`
* Version 9
  * `sudo dnf install -y bzip2 bzip2-devel expat-devel ncurses-devel openssl-devel readline-devel wget sqlite-devel tk-devel xz-devel zlib-devel libffi-devel`
  * NOTE: gdbm-devel package/module errored out for CentOS 9 and is not needed to complete steps below
* `wget https://www.python.org/ftp/python/3.10.4/Python-3.10.4.tgz`
  * Note: Make sure to download the latest version
  * Adjust the version numbers below with the latest version retrieved
* `tar -xf Python-3.10.4.tgz`
* `cd Python-3.10.4`
* `./configure --enable-optimizations`
  * **WAIT FOR THIS TO FINISH**
* `nproc` (Displays the number of cores in your processor)
  * NOTE: the number of cores on your system
* `make -j 4`
  * NOTE: the 4 in the command above is the number of cores on the system; yours may vary depending on what you have on your system
  * **WAIT FOR THIS TO FINISH**
* `sudo make altinstall`
  * **WAIT FOR THIS TO FINISH**
  * **DO NOT `sudo make install` AS IT WILL OVERWRITE THE DEFAULT SYSTEM PYTHON**
* `sudo dnf install -y python3-devel` **THIS IS NEEDED FOR SOME OF THE PYTHON MODULES**
* `python3.10 --version`
* `pip3.10 --version`
* Upgrade pip version
  * `/usr/local/bin/python3.10 -m pip install --upgrade pip`
* Installing modules for Python
  * [Pandas](https://pypi.org/project/pandas/)
    * `pip3.10 install pandas`
      * **WAIT FOR THIS TO FINISH**
  * [SQLAlchemy](https://pypi.org/project/SQLAlchemy/)
    * `pip3.10 install sqlalchemy`
  * [psycopg2](https://pypi.org/project/psycopg2/)
    * `pip3.10 install psycopg2-binary`
  * **Need to perform the following first before pyodbc and mysqlclient can be installed**
   * [Install dependencies for python3 and mysql](https://stackoverflow.com/questions/21530577/fatal-error-python-h-no-such-file-or-directory)
   * `sudo dnf install -y python3-devel mysql-devel unixODBC-devel` **IMPORTANT NOTE Install MariaDB first then do this command**
     * [pyodbc](https://pypi.org/project/pyodbc/)
       * `pip3.10 install pyodbc`
     * [mysqlclient](https://pypi.org/project/mysqlclient/)
       * `pip3.10 install mysqlclient`
         * If "NameError: name '\_mysql' is not defined", then proceed with the following instead
           * `pip3.10 uninstall mysqlclient`
           * `pip3.10 install --no-binary mysqlclient mysqlclient`
             * Note: The first occurrence is the name of the package to apply the no-binary option to, the second specifies the package to install
  * [Gunicorn](https://pypi.org/project/gunicorn/)
    * `pip3.10 install gunicorn`
