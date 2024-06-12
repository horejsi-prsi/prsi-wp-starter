# Zerops Hello WordPress

## Add new website

```yaml
#yamlPreprocessor=on
services:
  - hostname: websitename
    type: php-nginx@8.1
    buildFromGit: https://github.com/horejsi-prsi/prsi-wp-starter
    enableSubdomainAccess: true
    envSecrets:
      WORDPRESS_TITLE: WordPress on Zerops
      WORDPRESS_URL: ${zeropsSubdomain}

      WORDPRESS_ADMIN_EMAIL: "michal.horejsi@gmail.com"
      WORDPRESS_ADMIN_USER: admin
      WORDPRESS_ADMIN_PASSWORD: <@generateRandomString(<8>)>

      WORDPRESS_DEBUG: "false"
      WORDPRESS_DEBUG_DISPLAY: "false"
      WORDPRESS_DEBUG_LOG: "false"

      WORDPRESS_DB_HOST: ${db_hostname}
      WORDPRESS_DB_NAME: ${hostname}_prod
      WORDPRESS_DB_PASSWORD: ${db_password}
      WORDPRESS_DB_USER: ${db_user}
      WORDPRESS_TABLE_PREFIX: wp_

      WORDPRESS_STORAGE_ACCESS_KEY: ${storage_secretAccessKey}
      WORDPRESS_STORAGE_BUCKET: ${storage_bucketName}
      WORDPRESS_STORAGE_KEY_ID: ${storage_accessKeyId}
      WORDPRESS_STORAGE_URL: ${storage_apiUrl}

      WORDPRESS_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_AUTH_SALT: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_KEY: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_SALT: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_KEY: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_SALT: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_SALT: <@generateRandomString(<64>)>

      WORDPRESS_REDIS_USER_SESSION_HOST: ${redis_hostname}
      WFAF_STORAGE_ENGINE: mysqli
```


## Import full project

```yaml
#yamlPreprocessor=on
project:
  name: zerops-wordpress-project
services:
  - hostname: websitename
    type: php-nginx@8.1
    buildFromGit: https://github.com/horejsi-prsi/prsi-wp-starter
    enableSubdomainAccess: true
    envSecrets:
      WORDPRESS_TITLE: WordPress on Zerops
      WORDPRESS_URL: ${zeropsSubdomain}

      WORDPRESS_ADMIN_EMAIL: "michal.horejsi@gmail.com"
      WORDPRESS_ADMIN_USER: admin
      WORDPRESS_ADMIN_PASSWORD: <@generateRandomString(<8>)>

      WORDPRESS_DEBUG: "false"
      WORDPRESS_DEBUG_DISPLAY: "false"
      WORDPRESS_DEBUG_LOG: "false"

      WORDPRESS_DB_HOST: ${db_hostname}
      WORDPRESS_DB_NAME: ${hostname}_prod
      WORDPRESS_DB_PASSWORD: ${db_password}
      WORDPRESS_DB_USER: ${db_user}
      WORDPRESS_TABLE_PREFIX: wp_

      WORDPRESS_STORAGE_ACCESS_KEY: ${storage_secretAccessKey}
      WORDPRESS_STORAGE_BUCKET: ${storage_bucketName}
      WORDPRESS_STORAGE_KEY_ID: ${storage_accessKeyId}
      WORDPRESS_STORAGE_URL: ${storage_apiUrl}

      WORDPRESS_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_AUTH_SALT: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_KEY: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_SALT: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_KEY: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_SALT: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_SALT: <@generateRandomString(<64>)>

      WORDPRESS_REDIS_USER_SESSION_HOST: ${redis_hostname}
      WFAF_STORAGE_ENGINE: mysqli

  - hostname: dev1
    type: php-nginx@8.1
    buildFromGit: https://github.com/horejsi-prsi/prsi-wp-starter
    enableSubdomainAccess: true
    envSecrets:
      WORDPRESS_TITLE: WordPress on Zerops
      WORDPRESS_URL: ${zeropsSubdomain}

      WORDPRESS_ADMIN_EMAIL: "michal.horejsi@gmail.com"
      WORDPRESS_ADMIN_USER: admin
      WORDPRESS_ADMIN_PASSWORD: 123admin

      WORDPRESS_DEBUG: "true"
      WORDPRESS_DEBUG_DISPLAY: "true"
      WORDPRESS_DEBUG_LOG: "true"

      WORDPRESS_DB_HOST: ${db_hostname}
      WORDPRESS_DB_NAME: ${hostname}_dev
      WORDPRESS_DB_PASSWORD: ${db_password}
      WORDPRESS_DB_USER: ${db_user}
      WORDPRESS_TABLE_PREFIX: wp_

      WORDPRESS_STORAGE_ACCESS_KEY: ${storage_secretAccessKey}
      WORDPRESS_STORAGE_BUCKET: ${storage_bucketName}
      WORDPRESS_STORAGE_KEY_ID: ${storage_accessKeyId}
      WORDPRESS_STORAGE_URL: ${storage_apiUrl}

      WORDPRESS_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_AUTH_SALT: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_KEY: <@generateRandomString(<64>)>
      WORDPRESS_LOGGED_IN_SALT: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_KEY: <@generateRandomString(<64>)>
      WORDPRESS_NONCE_SALT: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_KEY: <@generateRandomString(<64>)>
      WORDPRESS_SECURE_AUTH_SALT: <@generateRandomString(<64>)>

      WORDPRESS_REDIS_USER_SESSION_HOST: ${redis_hostname}
      WFAF_STORAGE_ENGINE: mysqli

  - hostname: storage
    type: object-storage
    objectStorageSize: 2
    objectStoragePolicy: public-read
    pririty: 10

  - hostname: redis
    type: keydb@6
    mode: NON_HA
    priority: 10

  - hostname: db
    type: mariadb@10.6
    mode: NON_HA
    priority: 10

  - hostname: adminer
    type: php-apache@8.0+2.4
    buildFromGit: https://github.com/zeropsio/recipe-adminer@main
    enableSubdomainAccess: true
```
