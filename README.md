# stackit-internal-lb-poc

## Specifying node instance types

One can choose specific instance types for worker and control plane nodes by changing the following local
variables in [main.tf](./main.tf):
- `instance_type_worker`: Instance type for the worker nodes.
- `instance_type_control_plane`: Instance type for the control plane nodes.

> [!IMPORTANT]
> Note that both control plane and worker nodes need to use confidential instance types.

## Specifying node IP range

The IP range for the subnet used by Constellation's nodes can be set through the `cidr_vpc_subnet_nodes`
local variable in [main.tf](./main.tf). It needs to be ensured that this does not interfere with the
`192.168.177.0/24` range used by the STACKIT load balancer. If this range needs to be used by the nodes,
the range for the STACKIT load balancer needs to be adjusted and vice versa.

## Specifying load balancer ACLs

Until STACKIT offers pinning a load balancer to a static private IP address, ACLs should serve as a
workaround for prohibiting public access to the load balancer. In addition to the node and LB subnets,
which always need to be able to reach the load balancer, additional IP ranges that should be able to talk
to the load balancer can be specified through the option `extra_acl` in [main.tf](./main.tf).

The load balancer ACL feature needs to be enabled via the `enable_acl` option.
