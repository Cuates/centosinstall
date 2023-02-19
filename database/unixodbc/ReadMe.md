[How To Install unixodbc on Ubuntu 22.04](https://installati.one/install-unixodbc-ubuntu-22-04/)<br />

* Update system
  * `sudo apt-get update`
* Install unixodbc
  * `sudo apt-get -y install unixodbc`

* Modify /etc/odbcinst.ini File
  * `sudo vim /etc/odbcinst.ini`
    * Add to file
      * <pre>
        # ODBC Trace
        [ODBC]
        Trace           = no
        # Trace         = yes # Change this to yes if you want logs
        TraceFile       = /tmp/unixodbc.log
        </pre>
  * `sudo vim /etc/odbc.ini`
    * Add to file
      * <pre>
        [MSSQL]
        Driver          = FreeTDS
        Description     = MS SQL Server 2019
        Trace           = no
        Servername      = FreeTDS_Name
        Port            = 1433
        Database        = DATABASENAME
        UID             = USERNAME
        PWD             = PASSWORD
        TDS_Version     = 8.0
        </pre>
  * Save and Exit
* `isql --version`
* `isql -v <FreeTDS_Name> <username> <password>`
