

## SMB

runs on ports 139 and 445 usually

RPC CLIENT CONNECT AS ANONYMOUS
List all SMB shares
smbclient -N -L //10.129.14.128


rpcclient -U "" 10.129.14.128

The `rpcclient` offers us many different requests with which we can execute specific functions on the SMB server to get information. A complete list of all these functions can be found on the [man page](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) of the rpcclient.

| **Query**                 | **Description**                                                    |
| ------------------------- | ------------------------------------------------------------------ |
| `srvinfo`                 | Server information.                                                |
| `enumdomains`             | Enumerate all domains that are deployed in the network.            |
| `querydominfo`            | Provides domain, server, and user information of deployed domains. |
| `netshareenumall`         | Enumerates all available shares.                                   |
| `netsharegetinfo <share>` | Provides information about a specific share.                       |
| `enumdomusers`            | Enumerates all domain users.                                       |
| `queryuser <RID>`         | Provides information about a specific user.                        |





We can then use the results to identify the group's RID, which we can then use to retrieve information from the entire group.

#### Rpcclient - Group Information

SMB

```shell-session
rpcclient $> querygroup 0x201

        Group Name:     None
        Description:    Ordinary Users
        Group Attribute:7
        Num Members:2
```


Bruteforcing User RIDS 

use An alternative to this would be a Python script from [Impacket](https://github.com/SecureAuthCorp/impacket) called [samrdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py).

RIDS are user Ids.


```shell-session
samrdump.py 10.129.14.128
```

Another tool worth mentioning is the so-called [enum4linux-ng](https://github.com/cddmp/enum4linux-ng), which is based on an older tool, enum4linux. This tool automates many of the queries, but not all, and can return a large amount of information.






## NFS 

#### Show Available NFS Shares

NFS

```shell-session
JackTheWizard@htb[/htb]$ showmount -e 10.129.14.128

Export list for 10.129.14.128:
/mnt/nfs 10.129.14.0/24
```

#### Mounting NFS Share

NFS

```shell-session
JackTheWizard@htb[/htb]$ mkdir target-NFS
JackTheWizard@htb[/htb]$ sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
JackTheWizard@htb[/htb]$ cd target-NFS
JackTheWizard@htb[/htb]$ tree .

.
└── mnt
    └── nfs
        ├── id_rsa
        ├── id_rsa.pub
        └── nfs.share

2 directories, 3 files
```


MAKE SURE TO 
NFS

```shell-session
JackTheWizard@htb[/htb]$ cd ..
JackTheWizard@htb[/htb]$ sudo umount ./target-NFS


