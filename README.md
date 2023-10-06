# Development/testing environment for RHTAP Logging

# Assumptions

The setup was tested against a Quickcluster cluster and instructions assume the use of it.

# Prerequisites

As Splunk requires storage, a PV is required.
The [setup-nfs-quickcluster.sh](https://github.com/redhat-appstudio/infra-deployments/blob/main/hack/quickcluster/setup-nfs-quickcluster.sh) must run to setup NFS against the cluster.

# Deployment

1. ```console
   oc apply -f deploy-splunk.yaml
   ```
   
2. ```console
   oc apply -f install-external-secrets-operator.yaml
   ```

3. ```console
   oc apply -f install-openshift-logging-operator.yaml
   ```

4. ```console
   oc apply -f logging-configuration.yaml
   ```


**Note:** This manual process will be replace by an Argo CD deployment. 

# Checking the logs
1. `oc project splunk`
2. `oc get route splunk-web --template='{{.spec.host}}`
3. Copy the URL into your browser.\
   The user is `admin` and the password is `Password`.
4. Run a Splunk query against the index `rh_rhtap_dev_audit` or `rh_rhtap_dev_app`.