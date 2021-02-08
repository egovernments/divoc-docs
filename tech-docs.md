---
description: Relevant Software and Developer Documentation
---

# Tech Docs

## Developer Docs

1. [Admin API \(swagger\)](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#/admin-portal.yaml)
2. [Vaccination API \(swagger\)](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#/vaccination-api.yaml)
3. [Verification API \(swagger\)](https://egovernments.github.io/DIVOC/developer-docs/api/admin-api.html#/divoc-verification.yaml)

### Getting Started

In this section, we'll walk you through how to run DIVOC project on a local machine.

1. Install Docker Compose. Instructions can be found [here](https://docs.docker.com/compose/install/)

   **Basic Docker Compose Commands**

   * Staring services [`docker-compose up`](https://docs.docker.com/compose/reference/up/)
   * Restarting services [`docker-compose restart`](https://docs.docker.com/compose/reference/restart/)
   * Checking Status of services [`docker-compose ps`](https://docs.docker.com/compose/reference/ps/)
   * Monitoring service logs [`docker-compose logs`](https://docs.docker.com/compose/reference/logs/)

2. Clone DIVOC repository onto your local machine and navigate to `DIVOC` directory

   ```text
   git clone git@github.com:egovernments/DIVOC.git && cd DIVOC
   ```

3. Start all services in detached mode

   ```text
   docker-compose up -d
   ```

   * [Verify the state of containers](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-ps). All containers should be up.
   * Some services might fail to start because the dependent service might not be ready yet. [Restarting the failed service](https://github.com/egovernments/DIVOC/blob/main/docs/developer-docs/index.md#docker-compose-restart) should start it successfully in this case.
   * On Mac/Windows services might crash with exit code : 137, if sufficient memory is not set for docker. This can be changed in Docker desktop preferences, resources tab as shown [here](https://docs.docker.com/docker-for-mac/#resources).

4. Explore DIVOC

   Below are routes to access local apps. Remaining routes can be found in `nginx/nginx.conf`

   | Address | Application |
   | :--- | :--- |
   | localhost | public app |
   | localhost/portal | portal app |
   | localhost/facility\_app | facility app |

#### 

## Software Docs

### End User Guide <a id="demo-videos"></a>

{% file src=".gitbook/assets/1.-vesion-1.0-end-user-guide\_divoc.pdf" caption="Version 1.0" %}

### Implementation Guide <a id="demo-videos"></a>

Coming soon …

Currently DIVOC is in Beta mode. DIVOC team is constantly updating software documentation and will be made available through this page.

[Report issues and suggest features here](https://github.com/egovernments/DIVOC/issues)

[Ask questions and discuss here](https://github.com/egovernments/DIVOC/discussions)





