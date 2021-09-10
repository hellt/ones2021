This repo augments the [Containerlab](https://containerlab.srlinux.dev) demo given at Open Networking and Edge Summit 2021.

It contains the files needed to deploy a BGP Route Reflection lab built with containerlab.

![pic](https://gitlab.com/rdodin/pics/-/wikis/uploads/7fb73b48cfca59e0c07bbfe79180617c/image.png)

## Deploying a lab
Clone this repository, change into `ones2021` directory and execute

```
containerlab deploy -t rr.clab.yml
```

## Executing the use case
Once the lab deployment finishes, make goBGP peer to announce its route by doing:

```
docker exec clab-rr-gobgp bash /gobgp.sh
```

## Verifying route reflection operation
On SR Linux node, check that the route announced by goBGP has been received via Arista cEOS acting as a route reflector:

```
docker exec clab-rr-srlinux sr_cli "show network-instance default protocols bgp neighbor 192.168.11.2 received-routes ipv4"
```

## Destroying a lab
Do `containerlab destroy -t rr.clab.yml`
