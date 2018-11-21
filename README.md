# practice-envoyproxy
Envoyproxy practice with docker


Most read:
- https://www.paradigmadigital.com/dev/envoy-1-2-buceando-en-el-plano-de-datos-de-service-mesh/
- https://github.com/paradigmadigital/envoy

Create new cluster

$ curl --header "Content-Type: application/json" \
  --request PUT \
  --data @update_cluster.json \
  http://cds:3000/cluster/service1
  
  
  
  Add hosts to the cluster
$ cat > update_cluster.json << EOF
{
  "name": "service1",
  "connect_timeout": "1s",
  "lb_policy": "round_robin",
  "type": "strict_dns",
  "hosts": [
    {
      "socket_address": {
        "address": "host1",
        "port_value": 80
      }
    },
    {
      "socket_address": {
        "address": "host2",
        "port_value": 80
      }
    },
    {
      "socket_address": {
        "address": "host3",
        "port_value": 80
      }
    }
  ]
}
EOF

$ curl --header "Content-Type: application/json" \
  --request PUT \
  --data @update_cluster.json \
  http://cds:3000/cluster/service1
  

 Delete cluster
$ curl --header "Content-Type: application/json" \
  --request DELETE \
  http://cds:3000/cluster/service1
  
  
  Building the Control Plane for Service Discovery
  - We will be using consul, Nomad etc
  Help materials
  - https://sreeninet.wordpress.com/2016/04/17/service-discovery-with-consul/
  
  For sample REST crafting, use the proto3 documentation to craft a proper json for CDS, EDS or RDS
  - https://github.com/envoyproxy/data-plane-api/tree/master/envoy/api/v2
