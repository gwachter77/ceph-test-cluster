# Vagrant setup for a Ceph test cluster

Install Ceph Kraken on all nodes:
```sh
ceph-deploy new ceph-osd1 ceph-osd2 ceph-osd3
ceph-deploy install --release kraken --no-adjust-repo ceph-osd1 ceph-osd2 ceph-osd3
ceph-deploy mon create-initial
ceph-deploy osd prepare ceph-osd1:/var/local/osd ceph-osd2:/var/local/osd ceph-osd3:/var/local/osd
ceph-deploy osd activate ceph-osd1:/var/local/osd ceph-osd2:/var/local/osd ceph-osd3:/var/local/osd
ceph-deploy admin ceph-osd1 ceph-osd2 ceph-osd3
```
