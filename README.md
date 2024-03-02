# erpnext-15-Installation-on-docker

Clone and change directory to frappe_docker directory

```
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
```

Copy example devcontainer config from devcontainer-example to .devcontainer
Copy example vscode config for devcontainer from development/vscode-example to development/.vscode. This will setup basic configuration for debugging.

```
cp -R devcontainer-example .devcontainer
cp -R development/vscode-example development/.vscode
```


### Open the vscode remote container and follow the below command

```
nvm use v18
PYENV_VERSION=3.10 bench init --skip-redis-config-generation --frappe-branch version-15 frappe-bench
cd frappe-bench
```

```
bench set-config -g db_host mariadb
bench set-config -g redis_cache redis://redis-cache:6379
bench set-config -g redis_queue redis://redis-queue:6379
bench set-config -g redis_socketio redis://redis-socketio:6379
```

```
bench new-site s15.localhost --mariadb-root-password 123 --admin-password admin --no-mariadb-socket
bench use s15.localhost
```

```
bench set-config developer_mode 1
bench clear-cache
````

```
bench get-app --branch version-15 --resolve-deps erpnext
bench install-app erpnext
```

```
bench get-app --branch version-15 hrms
bench install-app hrms
```

```
bench get-app --branch version-15 payments
bench install-app payments
```

```
bench get-app --branch staging-14 https://github.com/thiruk-softsuave/ss_custom_erpnext.git
bench install-app ss_custom_erpnext
```

```
bench use s15.localhost
bench restore
```

```
bench migrate
bench build
```

