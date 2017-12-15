압축 해제
========

```bash
$ unzip linuxamd64_12102_client.zip
```

```
UNIX_GROUP_NAME=dba
SELECTED_LANGUAGES=en,ko
ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
ORACLE_BASE=/u01/app/oracle
oracle.install.client.installType=Runtime
```

```
$ ./runInstaller -noconsole -silent -force -waitforcompletion -responseFile /tmp/client/response/client_install.rsp
Starting Oracle Universal Installer...

Checking Temp space: must be greater than 415 MB.   Actual 8041 MB    Passed
Checking swap space: must be greater than 150 MB.   Actual 2047 MB    Passed
Preparing to launch Oracle Universal Installer from /tmp/OraInstall2017-01-09_03-29-32PM. Please wait ...
$
```
