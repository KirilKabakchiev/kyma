---
title: Configure Helm Broker
type: Configuration
---

The Helm Broker fetches bundle definitions from an HTTP server defined in the `values.yaml` file. The **config.repository.baseURL** attribute defines the HTTP server URL.

### Configuring the Helm Broker externally

Follow these steps to change the configuration and make the Helm Broker fetch bundles from a custom HTTP server:

1. Create a remote bundles repository. Your remote bundle repository must include the following resources:
    - An `index.yaml` file which defines available bundles.
      This file must have the following structure:

      ```text
      apiVersion: v1
      entries:
        {bundle_name}:
          - name: {bundle_name}
            description: {bundle_description}
            version: {bundle_version}
      ```
      This is an example of an `index.yaml` file for the Redis bundle:
      ```text
      apiVersion: v1
      entries:
        redis:
          - name: redis
            description: Redis service
            version: 0.0.1
      ```

    - A `{bundle_name}-{bundle_version}.tgz` file for each bundle version defined in the `index.yaml` file. The `.tgz` file is an archive of your bundle's directory.

2. In the `values.yaml` provide your server's URL in the **config.repository.baseURL** attribute:

  ```yaml
  config:
    repository:
      baseURL: "http://custom.bundles-repository"
  ```

3. Install Kyma on Minikube. See the **Local Kyma installation** document to learn how.
