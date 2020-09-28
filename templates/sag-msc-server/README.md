<!-- Copyright 2013 - 2018 Software AG, Darmstadt, Germany and/or its licensors

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

# Microservices Runtime

Use this template to provision and maintain Microservices Runtime

## Requirements

None.

### Supported Software AG releases

* Command Central 10.5 and higher
* Microservices Runtime 10.5 and higher

### Supported platforms

All supported Windows and UNIX platforms.

### Supported use cases

* Provisioning of new 10.5 or higher environments
* Installing latest fixes and support patches
* Configuration of:
  * License


## Provisioning of new server instance

For information about applying templates, see [Applying template using Command Central CLI](https://github.com/SoftwareAG/sagdevops-templates/wiki/Using-default-templates#applying-template-using-command-central-cli).

To provision a `default` instance of Microservices Runtime 10.5 with all latest fixes, using license key alias `MSC_LIC`
on a managed installation node alias `dev1`:

```bash
sagcc exec templates composite apply sag-msc-server nodes=dev1 \
  repo.product=webMethods-10.5 \
  repo.fix=Empower \
  msc.license.key=MSC_LIC \
  --sync-job --wait 360
  
To provision a `default` instance of Microservices Runtime 10.5 + layer product WmSAP with all latest fixes, using license key alias `MSC_LIC`
on a managed installation node alias `dev1`:

```bash
sagcc exec templates composite apply sag-msc-server nodes=dev1 \
  repo.product=webMethods-10.5 \
  repo.fix=Empower \
  msc.products=[MSC,WmSAP] \
  msc.license.key=MSC_LIC \
  --sync-job --wait 360
  
```
