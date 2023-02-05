# Hadoop & Monk
This repository contains Monk.io template to deploy Hadoop either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/monk-io/hadoop
```

## Load Template
```bash
cd hadoop
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list hadoop
✔ Got the list
Type      Template          Repository  Version  Tags
runnable  hadoop/hadoop  local       -        -
group     hadoop/stack   local       -        -

```

## Deploy Stack
```bash
foo@bar:~$ monk run hadoop/stack
? Select tag to run [local/hadoop/stack] on: mnk
✔ Starting the job: local/hadoop/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8 mnk-1
✔ [================================================] 100% bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8 mnk-1
✔ [================================================] 100% bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8 mnk-1
✔ [================================================] 100% bde2020/hadoop-historyserver:2.0.0-hadoop3.2.1-java8 mnk-1
✔ [================================================] 100% bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8 mnk-1
✔ Checking/pulling images DONE
✔ Started local/hadoop/stack

🔩 templates/local/hadoop/stack
 └─🧊 Peer mnk-1
    ├─🔩 templates/local/hadoop/hadoop
    │  └─📦 67e89e5f59f3a14cd83a79df2e196f1e-p-hadoop-hadoop-name-node
    │     ├─🧩 bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8
    │     ├─💾 /var/lib/monkd/volumes/hadoop/namenode -> /hadoop/dfs/name
    │     ├─🔌 open 13.53.139.95:9000 (0.0.0.0:9000) -> 9000
    │     └─🔌 open 13.53.139.95:9870 (0.0.0.0:9870) -> 9870
    ├─🔩 templates/local/hadoop/hadoop
    │  └─📦 f0037c35cd52a184fc1b1210675fceee-nk-hadoop-resourcemanager-node
    │     └─🧩 bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8
    ├─🔩 templates/local/hadoop/hadoop
    │  └─📦 b4861a80970424fcdada0f87372b066a-p-hadoop-hadoop-data-node
    │     ├─🧩 bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8
    │     └─💾 /var/lib/monkd/volumes/hadoop/datanode -> /hadoop/dfs/name
    ├─🔩 templates/local/hadoop/hadoop
    │  └─📦 95f606db5e8e8cfc5939c63be32554d4-hadoop-historyserver-node
    │     └─🧩 bde2020/hadoop-historyserver:2.0.0-hadoop3.2.1-java8
    └─🔩 templates/local/hadoop/hadoop
       └─📦 3a1beda66afeaf5a56562911df8117c8-p-hadoop-nodemanager-node
          └─🧩 bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/hadoop/stack - Inspect logs
	monk shell     local/hadoop/stack - Connect to the container's shell
	monk do        local/hadoop/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```
 
 ## Open Web Ui
 ```
http://13.53.139.95:9870
```


## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| kong_database_name            | Kong database name, Default: kong 	               |
| kong_database_password        | Kong database password, Default kong                     	|
| kong_database_user            | Kong database user, Default: kong                     	|
| kong_database_port            | Kong database port, Default: 5432                     	|
| kong_proxy_listen             | Kong Proxy listen, Default 8000                     	|
| kong_admin_listen               | Kong admin listen, Default 8001                     	|
| konga_admin_listen               | Konga port Default: 1337                     	|



## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```

