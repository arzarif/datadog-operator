# Getting Started

This procedure describes the simplest and fastest way to deploy the Datadog agent with the operator.
For a more complete description of a more versatile way to install the operator and configure the agent it deploys, please refer to the [Installation guide](installation.md).

## Prerequisites

Using the Datadog Operator requires the following prerequisites:

- **Kubernetes Cluster version >= v1.14.X**: Tests were done on versions >= `1.14.0`. Still, it should work on versions `>= v1.11.0`. For earlier versions, due to limited CRD support, the operator may not work as expected.
- [`Helm`][1] for deploying the `Datadog-operator`.
- [`Kubectl` cli][2] for installing the `Datadog-agent`.

## Deploy an agent with the operator

In order to deploy a Datadog agent with the operator in the minimum number of steps, the [`datadog-agent-with-operator`](https://github.com/DataDog/datadog-operator/tree/master/chart/datadog-agent-with-operator) helm chart can be used.
Here are the steps:

1. [Download the chart][3]:

   ```shell
   curl -Lo datadog-agent-with-operator.tar.gz https://github.com/DataDog/datadog-operator/releases/latest/download/datadog-agent-with-operator.tar.gz
   ```

2. Create a file with the spec of your agent. The simplest configuration is:

   ```yaml
   credentials:
     apiKey: <DATADOG_API_KEY>
     appKey: <DATADOG_APP_KEY>
   agent:
     image:
       name: "datadog/agent:latest"
   ```

   Replace `<DATADOG_API_KEY>` and `<DATADOG_APP_KEY>` with your [Datadog API and application keys][4]

3. Deploy the Datadog agent with the above configuration file:
   ```shell
   helm install --set-file agent_spec=/path/to/your/datadog-agent.yaml datadog datadog-agent-with-operator.tar.gz
   ```

## Cleanup

The following command deletes all the Kubernetes resources created by the above instructions:

```shell
kubectl delete datadogagent datadog
helm delete datadog
```

[1]: https://helm.sh
[2]: https://kubernetes.io/docs/tasks/tools/install-kubectl/
[3]: https://github.com/DataDog/datadog-operator/releases/latest/download/datadog-agent-with-operator.tar.gz
[4]: https://app.datadoghq.com/account/settings#api
