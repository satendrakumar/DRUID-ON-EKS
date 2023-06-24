#### Please create node group with 5 * m5.large nodes on EKS than start these steps.

#### create namespace for druid cluster:
     $ kubectl create namespace druid
#### Install the zookeeper:
      $ helm install zookeeper  -n druid  -f zookeeper/values.yaml   oci://registry-1.docker.io/bitnamicharts/zookeeper

#### Update the zookeeper cluster after config change:
    $ helm upgrade zookeeper  -n druid  -f values.yaml   oci://registry-1.docker.io/bitnamicharts/zookeeper

##### install druid operator
    $ kubectl create namespace druid-operator
    $ helm -n druid-operator install cluster-druid-operator -f druid-operator/chart/values.yaml  ./druid-operator/chart

##### Install druid cluster:
      $ kubectl apply -f druid-cluster/dev-cluster.yaml -n druid