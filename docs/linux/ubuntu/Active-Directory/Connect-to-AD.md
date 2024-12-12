# Connect Ubuntu Server to Active Directory

1. First we need to install some packages
```bash
sudo apt install winbind libnss-winbind libpam-winbind
```

2. Now we double check that our network settings are correct
```bash
resolvectl status
```

3. Now we need to edit our Configurations
```bash
sudo nano /etc/samba/smb.conf
```
Under the `[global]` section paste this
```conf
    security = ads
    realm = RTECH.ORG
    workgroup = RTECH

    idmap config * : backend       = tdb
    idmap config * : range         = 100000 - 199999
    idmap config EXAMPLE : backend = rid
    idmap config EXAMPLE : range   = 1000000 - 1999999

    # allow logins when the DC is unreachable
    winbind offline logon = yes
    # this *can* be yes if there is absolute certainty that there is only a
    # single domain involved
    winbind use default domain = no
    # setting these enumeration options to yes has a high performance impact
    # and can cause instabilities
    winbind enum groups = no
    winbind enum users = no
    winbind refresh tickets = yes
    # if domain users should be allowed to login, they will need a login shell
    template shell = /bin/bash
    # the home directory template for domain users
    template homedir = /home/%D/%U
    kerberos method = secrets and keytab
```

4. Now we need to test that
```bash
testparm
```