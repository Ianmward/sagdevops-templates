<!--
 Copyright (c) 2011-2019 Software AG, Darmstadt, Germany and/or Software AG USA Inc.,
 Reston, VA, USA, and/or its subsidiaries and/or its affiliates and/or their licensors.

 SPDX-License-Identifier: Apache-2.0

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
-->

# Creating webMethods database on Oracle

With this template you can create user, storage tablespaces and webMethods database components on an Oracle database server.

## Requirements

### Supported Software AG releases

* Command Central 10.1 and 10.3
* Database Component Configurator 9.10 to 10.3
* webMethods database components for products 9.8 to 10.3

### Supported platforms

* All supported Windows and UNIX platforms
* All supported versions of Oracle database
* Docker Engine 17.09 or higher

## Running as a standalone Composite Template

To install Database Component Configurator 10.1 on the Command Central node with alias `local`, create a database named `webm` and a database user named `webm` with password `webm`, and create database storage and database components for Integration Server 10.1 and My webMethods Server 10.1 with user `system` and password `oracle`:

```bash
sagcc exec templates composite apply sag-db-oracle-103-and-lower
  db.version=10.1.0.0 repo.product=products-10.1 repo.fix=fixes-10.1 nodes=local
  db.host=oracle db.admin.username=system db.admin.password=oracle
  db.name=webm db.username=webm db.password=webm
  db.products=[IS,MWS]
  --sync-job --wait 360
```

## Using for local development and testing on Docker platforms

1. Launch the Command Central container from the root folder of the following project:

```bash
docker-compose up -d cc
```

2. Launch the [Oracle Database Express Edition 11g Release 2](https://hub.docker.com/r/wnameless/oracle-xe-11g/) container:

```bash
docker-compose -f templates/sag-db-oracle-103-and-lower/docker-compose.yml up -d oracle
```

3. Provision the `sag-db-oracle-103-and-lower` template to create a user, storage, and Integration Server, My webMethods Server and BPM database components for the 10.3 release:

```bash
CC_ENV=oracle ./provisionw sag-db-oracle-103-and-lower
```
If the test is successful, the test ouptut contains `TEST SUCCESSFUL`.

You can now use this database for creating instances of webMethods products (for example, Integration Server and My webMethods Server) with the following database connection properties:

```bash
db.url=jdbc:wm:oracle://oracle:1521;SID=XE
db.username=webm
db.password=webm
db.type=oracle
```

The properties are pre-set in the `environments/oracle/env.properties` file and you can use them by pointing to the environment name, for example:

```bash
CC_ENV=oracle ./provisionw sag-optimize-analysis
```
