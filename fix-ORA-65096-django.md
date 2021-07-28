## Table of Contents
1. [Introduction](#Introduction)
2. [Finding clues](#Finding_clues)
3. [Solution](#Solution)
4. [References](#References)

Error: ORA-65096: invalid common user or role name in oracle

<h2 id='Introduction'>Introduction</h2>
Hello guys,
I'm new to backend and django, so i had decided to follow along with django tutorial

Here is some detail what i was using to meet and fix this error:
* Django version 3.2.5
* Database: Oracle Database Express Edition (XE) Release 18.4.0.0.0 (18c)
* Windows 11

Next semester, I have a course using Oracle so I decided to use Oracle instead of using Sqlite as the Django tutorial used
I've been struggling with this line '_ORA-65096: invalid common user or role name in oracle_' for two days
So I want to create this post as a guide for anyone who meet this problem as i am.

<h2 id='Finding_clues'>Finding clues</h2>

```powershell
python manage.py test polls
```

What we *should* get
```powershell
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_was_published_recently_with_future_question (polls.tests.QuestionModelTests)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/path/to/mysite/polls/tests.py", line 16, in test_was_published_recently_with_future_question
    self.assertIs(future_question.was_published_recently(), False)
AssertionError: True is not False

----------------------------------------------------------------------
Ran 1 test in 0.001s

FAILED (failures=1)
Destroying test database for alias 'default'...
```
What we actually get :(
```powershell
Creating test database for alias 'default'...
    Failed (ORA-01543: tablespace 'TEST_SYSTEM' already exists)
    It appears the test database, test_system, already exists. Type 'yes' to delete it, or 'no' to cancel: yes
    Destroying old test database for alias 'default'...
    Creating test user...
    Failed (ORA-65096: invalid common user or role name)
    Got an error creating the test user: ORA-65096: invalid common user or role name
```
So the program failed when trying to create a new user

Let's open sqlplus to create a new user manually, I get the same error when try to create new user
"ORA-65096: invalid common user or role name"

Why?
I am logging in as an administrator user with full privileges

And so, I do some researches and find out that
```powershell
SQL> show con_name

CON_NAME
------------------------------
CDB$ROOT
```
We are in the container 'CDB$ROOT', which is the keeper of all the PDBs that are part of the collection
PDB is a Pluggable database
All PDBs are plugged in CDB$ROOT, this structure is called a container database (CDB)
[learn more](https://logicalread.com/oracle-pluggable-databases-mc05/#.YQEj_44za3B)

Aside with those kind of headache, all we need to know is 
```word
99.9% of the time the error ORA-65096: invalid common user or role name means you are logged into the CDB when you should be logged into a PDB.
```

* So we need an user have con_name is PDB to create user on that PDB
```powershell
SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 XEPDB1                         READ WRITE NO
```
Here you can see there is a Pluggable database named XEPDB1, because I am using Oracle XE
If you are using Oracle 12 it will be ORCLPDB

[Go to solution to see how to create user with PDB](#Solution)


Here we go again, new error showed up
<p id='settings'>django.db.utils.DatabaseError: ORA-12505: TNS:listener does not currently know of SID given in connect descriptor</p>

Check settings.py file

```vim
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.oracle',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '1521',
    }
}
```
Try to login to sqlplus with the user we have just created
```powershell
PS D:\Workplace\Backend\mysite> sqlplus django/django

SQL*Plus: Release 18.0.0.0.0 - Production on Wed Jul 28 15:56:57 2021
Version 18.4.0.0.0

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

ERROR:
ORA-01017: invalid username/password; logon denied
```

Hmm, why???

I have tried to create an user with that same username, it says
```powershell
ORA-01920: user name 'DJANGO' conflicts with another user or role name
```
Why ????????

Do some research
Found out we cannot use users at Pluggable Database connect to root container

And how do we connect to a specific PDB though?

```word
You are connecting to root container by using sqlplus testtest/password where the user doesn't exist.
Instead, you can use EZConnect or you can create a TNS name to connect to the PDB.
```
Ok then learn something about ezconnect syntax
sqlplus username/password@hostname:port/pdbname

```powershell
PS D:\Workplace\Backend\mysite> sqlplus django/django@localhost:1521/XEPDB1

SQL*Plus: Release 18.0.0.0.0 - Production on Wed Jul 28 16:05:09 2021
Version 18.4.0.0.0

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

Last Successful login time: Wed Jul 28 2021 14:18:57 +07:00

Connected to:
Oracle Database 18c Express Edition Release 18.0.0.0.0 - Production
Version 18.4.0.0.0

SQL>
```
Try to create user
```powershell
SQL> create user test identified by test;

User created.
```
Perfect

But how do we tell django using this kind of syntax though, it keep throwing errors to my face

```word
The HOST and PORT keys need to be left out of the dictionary - else Django will try connecting with the complete "NAME" as an SID.
```
Ok then
Let try to login with service name instead
Try to login with service name in sqlplus
```powershell
PS D:\Workplace\Backend\mysite> sqlplus -L "django/django@(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=localhost)(PORT=1521))(CONNECT_DATA=(SERVICE_NAME=XEPDB1)))"

SQL*Plus: Release 18.0.0.0.0 - Production on Wed Jul 28 12:06:33 2021
Version 18.4.0.0.0

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

Last Successful login time: Wed Jul 28 2021 12:02:04 +07:00

Connected to:
Oracle Database 18c Express Edition Release 18.0.0.0.0 - Production
Version 18.4.0.0.0
```

Change settings.py a little bit

```powershell
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.oracle',
        'NAME': 'localhost:1521/XEPDB1',
        'USER': 'django',
        'PASSWORD': 'django',
    }
}
```

<h2 id='Solution'>Solution</h2>
* Connect to sqlplus as sys
```powershell
PS D:\Workplace\Backend\mysite> sqlplus "sys AS SYSDBA"

SQL*Plus: Release 18.0.0.0.0 - Production on Wed Jul 28 12:47:31 2021
Version 18.4.0.0.0

Copyright (c) 1982, 2018, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 18c Express Edition Release 18.0.0.0.0 - Production
Version 18.4.0.0.0
```
* Create PDB account
```powershell
SQL> alter session set container = XEPDB1;

Session altered.

SQL> create user django identified by django;

User created.

SQL> grant all privileges to django;

Grant succeeded.
```
* Create/Edit Database connection with that user
![databse-connection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p9gnrcjs3e4jti9rf76v.png)
_Remember to change service name to the container we have used above **If you're using Oracle 12, container will be ORCLPDB**, hit the connect button_
* Open file yoursite/yoursite/settings.py
```powershell
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.oracle',
        'NAME': 'localhost:1521/XEPDB1',
        'USER': 'django',
        'PASSWORD': 'django',
    }
}
```
If you meet this error, follow my guild here
[django.db.utils.DatabaseError: ORA-12505: TNS:listener does not currently know of SID given in connect descriptor](#settings)

*  Apply the migrations for app (again because we have connected to a new database)
```powershell
python manage.py migrate
```
* Run test
```powershell
PS D:\Workplace\Backend\mysite> python manage.py test polls
Creating test database for alias 'default'...
Creating test user...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_was_published_recently_with_future_question (polls.tests.QuestionModelTests)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "D:\Workplace\Backend\mysite\polls\tests.py", line 12, in test_was_published_recently_with_future_question
    self.assertIs(future_question.was_published_recently(), False)
AssertionError: True is not False

----------------------------------------------------------------------
Ran 1 test in 0.006s

FAILED (failures=1)
Destroying test database for alias 'default'...
Destroying test user...
Destroying test database tables...
```
* Succeed, thanks for reading

<h2 id='References'>References</h2>

[Tutorial link] (https://docs.djangoproject.com/en/3.2/intro/tutorial05/)
Blogs and stackoverflow-s that helped me through this error:
* <https://stackoverflow.com/questions/33330968/error-ora-65096-invalid-common-user-or-role-name-in-oracle>
* <https://logicalread.com/oracle-pluggable-databases-mc05/#.YQES444za3A>
* <https://dba.stackexchange.com/questions/196780/i-cannot-login-to-a-user-i-just-created-in-a-pdb>
* <https://stackoverflow.com/questions/19246643/how-do-i-force-django-to-connect-to-oracle-using-service-name>








