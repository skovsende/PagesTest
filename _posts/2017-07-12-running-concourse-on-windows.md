---
layout: post
title:  "Running concourse on Windows"
date:   2017-07-12 20:24:00 +0100
categories: concourse windows
---
Here follows a simple description of the steps I used to get [Concourse] up and running
on Windows Server 2016. I used an Azure virtual machine with Windows 2016 Datacenter -
with Containers as the base image.

### Installing chocolatey - (remove this?)

Start by running the following in an admin powershell:

```powershell
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### Installing PostgreSQL

Install [PostgreSQL] by installing from 
[here](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads#windows). 
I installed 9.6.3, but at the time of writing 9.3+ is supported. 

### Creating ssh keys
Concourse needs at least 3 ssh keys to get up and running. One for the signing user session tokens, 
one for the TSA server, and one per worker. I just used the ssh-keygen bundled with my
git installation. Create them without pass phrases.

```powershell
ssh-keygen -t rsa -f tsa_host_key
ssh-keygen -t rsa -f worker_key
ssh-keygen -t rsa -f session_signing_key
```

*TODO: Install pub key of worker. They are in c:\concourse atm*
*TODO: Open ports for Postgres - create db*

### Next step - run concourse

[Concourse]: http://concourse.ci/
[PostgreSQL]: https://www.postgresql.org/