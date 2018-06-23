# Virtual Private Cloud

## Quick pointers

- VPC is per region, Subnet is per Availability Zone.

- When creating VPC, 'DNS Hostnames' is disabled by default. This indicates if new instances launched in the VPC gets assigned public DNS hostnames.

- When creating subnet, 'Auto-assign Public IP' is disabled by default.

- When defining the route table, it's a good idea to leave the default (main) route table untouched and create new route tables to explicitly associate to subnets. This prevents accidentally having newly created subnets get assigned route tables that are not meant to be used.

- When launching an EC2 instance to a subnet, it gets a new public IP all the time. We don't want this and want to have some reliable IP that can be reused.

- Elastic IP can be associated to either EC2 Instance or Network interface.

- Internet Gateway - 1 per VPC, but 1 Gateway can be associated to many VPCs at the same time.

- DHCP Options - 1 per VPC, but 1 DHCP Options can be associated to many VPCs at the same time.
