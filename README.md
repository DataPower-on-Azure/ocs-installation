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
> Make sure you uninstall the osc/odf operator from your cluster before you sync again.
