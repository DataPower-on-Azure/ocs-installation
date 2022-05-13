- Manually update machinesets by copying the `resource group` & `image` from `worker nodes MACHINES` to our `MACHINESETS`
- Go Stop the `autosync` on the `Machinesets.yaml`
- Make sure to terminate the sync on argo FROM INSIDE THE STORAGE.
```bash
cd multi-tenancy-gitops-infra/storage/
```
- Find in `Chart.yaml` the url for the helm chart
- [Click here!](https://github.com/cloud-native-toolkit/toolkit-charts)

```bash
cd toolkit-charts/stable/ocs-operator/
```
- You will be able to find the correct charts for `ocs-operator`
- Copy Paste into your `ORG`
- Then Terminate argo & sync again.

> Note!
> Make sure you uninstall the ocs/odf operator from your cluster before you sync again.

> COPY OF THEM HERE
`Chart.yaml`
```yaml
apiVersion: v2
name: ocs-operator
description: A Helm chart for deploying infrastrucure reference architecture to OpenShift 4.x clusters

# A chart can be either an 'application' or a 'library' chart.
#
# Application charts are a collection of templates that can be packaged into versioned archives
# to be deployed.
#
# Library charts provide useful utilities or functions for the chart developer. They're included as
# a dependency of application charts to inject those utilities and functions into the rendering
# pipeline. Library charts do not define any templates and therefore cannot be deployed.
type: application

# This is the chart version. This version number should be incremented each time you make changes
# to the chart and its templates, including the app version.
# Versions are expected to follow Semantic Versioning (https://semver.org/)
version: 0.2.4

# This is the version number of the application being deployed. This version number should be
# incremented each time you make changes to the application. Versions are not expected to
# follow Semantic Versioning. They should reflect the version the application is using.
appVersion: 0.1.0
```
`values.yaml`
```yaml
# Default values for refarch-ocp4-gitops.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

channel: ""
sizeGiB: ""
storageClass: ""

infraNodes:
  taints: {}

storageNodes:
  taints: {}

argo:
  namespace: ""
  serviceAccount: ""

global:
  infraNodes:
    taints:
      - effect: "NoSchedule"
        key: "infra"
        value: ""
    labels:
      node-role.kubernetes.io/infra: ""
  storageNodes:
    taints:
      - effect: "NoSchedule"
        key: "node.ocs.openshift.io/storage"
        value: "true"
    labels:
      node-role.kubernetes.io/storage: ""
      cluster.ocs.openshift.io/openshift-storage: ""
  cloudpakNodes:
    taints:
    labels:
      node-role.kubernetes.io/cp4x: ""
```
