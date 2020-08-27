[How To Install Python 38 On CentOS 8](https://linuxize.com/post/how-to-install-python-3-8-on-centos-8/)<br />
[How To Install Python On 3 On CentOS](https://computingforgeeks.com/how-to-install-python-on-3-on-centos/)
* `sudo dnf groupinstall -y 'development tools'`
* `sudo dnf install -y bzip2 bzip2-devel expat-devel gdbm-devel ncurses-devel openssl-devel readline-devel wget sqlite-devel tk-devel xz-devel zlib-devel libffi-devel`
* `wget https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz`
* `tar -xf Python-3.8.5.tgz`
* `cd Python-3.8.5`
* `./configure --enable-optimizations`
* `nproc` (Displays the number of cores in your processor)
* `make -j 4`
  * **WAIT FOR THIS TO FINISH**
* `sudo make altinstall`
  * **WAIT FOR THIS TO FINISH**
  * **DO NOT `sudo make install` AS IT WILL OVERWRITE THE DEFAULT SYSTEM PYTHON**
* `sudo dnf install -y python3-devel` **THIS IS NEEDED FOR SOME OF THE PYTHON MODULES**
* `python3.8 --version`
* `pip3.8 --version`
* Upgrade pip version
  * `/usr/local/bin/python3.8 -m pip install --upgrade pip`
* Installing modules for Python
  * [SQLAlchemy](https://pypi.org/project/SQLAlchemy/)
    * `pip3.8 install sqlalchemy`
  * [psycopg2](https://pypi.org/project/psycopg2/)
    * `pip3.8 install psycopg2-binary`
  * **need to perform the following first before pyodbc and mysqlclient can be installed**
  * [Install dependencies for python3 and mysql](https://stackoverflow.com/questions/21530577/fatal-error-python-h-no-such-file-or-directory)
  * `sudo dnf install -y python3-devel mysql-devel`
    * [pyodbc](https://pypi.org/project/pyodbc/)
      * `pip3.8 install pyodbc`
    * [mysqlclient](https://pypi.org/project/mysqlclient/)
      * `pip3.8 install mysqlclient`
