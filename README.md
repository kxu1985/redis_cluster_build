# Build Redis Cluster

## Preparation
- Launch 6 AWS instances using Ubuntu 18.04
- Install Redis on all the nodes

## Configuration File
- This step is conducted on each node.
- Run
```
cat <<EOF | tee ./redis.conf
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
EOF
```
- Run `screen`
- Run `redis-server ./redis.conf --protected-mode no`
- Run `ctl+A+D` to detach the screen

## Create Cluster
- Run the following on one node
- Run `redis-cli --cluster create <ip1>:7000 <ip2>:7000 <ip3>:7000 <ip4>:7000 <ip5>:7000 <ip6>:7000 --cluster-replicas 1`

## Launch CLI
- Run `redis-cli -c -p 7000`

## Get Cluster Info
- Under CLI run `cluster nodes`
