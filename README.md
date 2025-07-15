## EDB: 

EnterpriseDB (EDB) is a global software company that provides enterprise-class products and services based on **PostgreSQL**, the world’s most advanced open-source relational database.

EDB aims to **help organizations run mission-critical workloads using PostgreSQL**, with the flexibility and freedom of open-source and the reliability of commercial-grade support.

**EDB-PostgreSQL**, developed by EnterpriseDB (EDB), is a **commercial offering built on top of open-source PostgreSQL**. It provides both the standard PostgreSQL distribution and an enhanced version called EDB Postgres Advanced Server (EPAS).


### What EDB Offers:

#### 1. EDB Postgres Advanced Server (EPAS):
- A hardened, enterprise-grade version of PostgreSQL
- Offers Oracle compatibility, performance tuning, and enhanced security
- Used by enterprises that want to replace Oracle with an open-source alternative

#### 2. EDB Tools and Solutions:
- Migration Toolkit: Migrate from Oracle, SQL Server, MySQL to PostgreSQL
- EDB Postgres Enterprise Manager (PEM): Monitoring and administration
- Backup & Recovery Tool (BART): Streamlined backups
- Failover Manager (EFM): HA and automatic failover
- Replication Server: For real-time data replication



### Key Features of EDB-PostgreSQL:

| Feature                  | Community PostgreSQL | EDB Postgres Advanced Server |
| ------------------------ | -------------------- | ---------------------------- |
| Open Source              | ✅ Yes                | ❌ Partial (some proprietary) |
| Oracle Compatibility     | ❌ No                 | ✅ Yes                        |
| Performance Enhancements | ⚠️ Limited            | ✅ Yes                        |
| EDB Tools & Support      | ❌ No                 | ✅ Yes (with subscription)    |
| Support Options          | Community only        | 24/7 enterprise-grade        |





---
---



## EDB repositories for Linux:

To install EDB Postgres Advanced Server (EPAS) 16 or 17 on Rocky Linux, you must create or login to an EDB account. EDB provides access to installers and repositories, but the exact **repo URL is not public**. You need to visit the EDB website, select Rocky Linux, and either copy the `dnf config-manager` command or download a personalized `.repo` file after logging in.



### Step-1: Add the EDB Repository: 

Select Platform: **Rocky/Alma/Oracle Linux 8 x86_64**


#### Auto: 

_Use this to quickly setup the repository automatically (**recommended**)._
```
curl -1sSLf 'https://downloads.enterprisedb.com/<your_token>/enterprise/setup.rpm.sh' | sudo -E bash
```


#### Manual:

_Configure the repository yourself before installing packages:_
```
dnf install yum-utils 

rpm --import 'https://downloads.enterprisedb.com/<your_token>/enterprise/gpg.E71EB0829F1EF813.key'

curl -1sSLf 'https://downloads.enterprisedb.com/<your_token>/enterprise/config.rpm.txt?distro=el&codename=' > /tmp/enterprise.repo

dnf config-manager --add-repo '/tmp/enterprise.repo'

dnf -q makecache -y --disablerepo='*' --enablerepo='enterprisedb-enterprise'
```


### Step-2: Install Database: 

Once the repository is configured, run this to install the software packages.

- **EDB Postgres Advanced Server**: Enterprise-ready, Postgres with Oracle Compatibility and TDE
- **PostgreSQL**: PostgreSQL, supported by EDB
- **EDB Postgres Enterprise Manager**: Manage, monitor, and optimize PostgreSQL
- **EDB Postgres Failover Manager**: High availability for PostgreSQL
- **EDB Postgres Replication Server**: Synchronize data to or from non-PostgreSQL, as well as, between PostgreSQL databases
- **EDB Connectors**: EDB Postgres Advanced Server connectors, including JDBC, ODBC, .NET, and OCL
- **EDB Barman**: Automate backup and recovery for PostgreSQL


_EDB Postgres Advanced Server v16:_
```
sudo dnf -y install edb-as16-server edb-pem edb-efm50 edb-xdb edb-jdbc
```


_EDB Postgres Advanced Server v17:_
```
sudo dnf -y install edb-as17-server edb-pem edb-efm50 edb-xdb edb-jdbc
```



#### Initialize Database: 

```
/usr/edb/as16/bin/edb-as-16-setup initdb
```


```
systemctl start edb-as-16
systemctl status edb-as-16
```


```
netstat -tlpn | grep edb

tcp        0      0 0.0.0.0:5444        0.0.0.0:*      LISTEN      96275/edb-postgres
```



#### Connect to Database: 

```
su - enterprisedb
```


```
psql edb
psql -d edb
psql -U enterprisedb -d edb
```


EnterpriseDB (EDB) is a leading provider of PostgreSQL-based database solutions tailored for enterprise needs.


