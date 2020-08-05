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
* `python3.8 --version`
* `pip3.8 --version`
