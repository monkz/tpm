# tpm.py

A Python Module for the [TeamPasswordManager API](http://teampasswordmanager.com/docs/api/)

Requires: requests

## Install tpm.py

You can install the tpm module via pip

    pip install tpm

## How to Use

This is an example how you can use it in a python script
```python
#! /usr/bin/env python
import tpm
# create a object for the connection settings
URL = "https://myPasswordManager.example.com"
API = "/index.php/api/v3/"
USER = 'MyUser'
PASS = 'Secret'
conn = tpm.Connection(API, URL, USER, PASS)

# get a dictionary for all password entries
data = tpm.getData(conn, 'passwords')
# show all names from the password entries
for item in data:
    print item.get('name')
```
## Functions explained
### Functions that get data from TeamPasswordManager
---
#### getData(conn, TYPE, SEARCHSTRING='')

*Connect to TPM and return found Entries in a List of Dictionaries.*

**TYPE** - Accepts 'passwords' or 'projects'.

**SEARCHSTRING** - optional, will return only values that are matching the SEARCHSTRING.

#### getDetailData(conn, TYPE, ID)

*Get more detailed data per entry, returns a single Dictionary.*

**TYPE** - Accepts 'passwords' or 'projects'.

**ID** - ID from the Entry you want more detailed informations.

#### getArchived(conn, TYPE)

*Return all archived entries from 'passwords' or 'projects'*

**TYPE** - Accepts 'passwords' or 'projects'.

#### getFavorite(conn, TYPE)

*Return all favorite entries from 'passwords' or 'projects'*

**TYPE** - Accepts 'passwords' or 'projects'.

#### getSecurity(conn, TYPE, ID)

*List Users that have Access to a specific entry by ID.*

**TYPE** - Accepts 'passwords' or 'projects'.

**ID** - ID from the Entry you want to get the Users that have Access.

#### generatePass(conn)

*Generates a random password from Team Password Manager.*

### Functions that create data to TeamPasswordManager
---
#### postData(conn, TYPE, DATA)

*Create a new entry in TeamPasswordManager.*

**TYPE** - Accepts 'passwords' or 'projects'.

**DATA** - Takes an dictionary, translate it to JSON and post it to the API, if fields are wrong, the API will complain.

### Functions that update data to TeamPasswordManager
---
#### putData(conn, TYPE, ID, DATA)

*Update an entry in TPM.*

**TYPE** - Accepts 'passwords' or 'projects'.

**ID** - ID from the Entry you want to update.

**DATA** - Takes an dictionary, translate it to JSON and post it to the API, if fields are wrong, the API will complain.

#### putSecurity(conn, TYPE, ID, DATA)

*Update Security Access for an entry.*

**TYPE** - Accepts 'passwords' or 'projects'.

**ID** - ID from the Entry you want to update.

**DATA** - Takes an dictionary, translate it to JSON and post it to the API, if fields are wrong, the API will complain.

#### putCustomFields(conn, ID, DATA)

*Update custom field labels for an entry.*

**ID** - ID from the entry you want to delete.

**DATA** - A dictionary that defines the custom fields e.g.:
```python
DATA = {'custom_label1': 'IP',
        'custom_type1': 'text',
        'custom_label2': 'CNAME',
        'custom_type2': 'text',
        'custom_label3': 'E-Mail',
        'custom_type3': 'email'}
```
#### lockPassword(conn, ID)

**ID** - ID from the entry you want to lock.

#### unlockPassword(conn, ID)

**ID** - ID from the entry you want to unlock.

**REASON** - The Reason why you want to unlock.

### Functions that delete data from TeamPasswordManager
---
#### deleteData(conn, TYPE, ID)

**TYPE** - Accepts 'passwords' or 'projects'.

**ID** - ID from the entry you want to delete.

## Examples
