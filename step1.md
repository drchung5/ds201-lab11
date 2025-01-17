<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Replication</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:academy@datastax.com">email</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 2</span>
 <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Configure the nodes</div>

The environment for this exercise consists of three cassandra nodes: *node1*, *node2* and *node3*

✅ Open `/workspace/ds201-lab11/node1/conf/cassandra.yaml` in a *nano* or the text editor of your choice and view the `endpoint_snitch` setting:

```
nano /workspace/ds201-lab11/node1/conf/cassandra.yaml
```

You should see *GossipingPropertyFileSnitch*. The default snitch, *SimpleSnitch* is only appropriate for single datacenter deployments. 

---
**Note:** *GossipingPropertyFileSnitch* should be your go-to snitch for production use.  The rack and datacenter for the local node are defined in *cassandra-rackdc.properties* and propagated to other nodes via Replication.

---

Verify that the `cassandra.yml` files for  *node2* and *node3* all use the same snitch.


✅ Open `/workspace/ds201-lab11/node1/conf/cassandra-rackdc.properties` in a *nano* or the text editor of your choice and find the `dc` and `rack` settings:
```
nano /workspace/ds201-lab11/node1/conf/cassandra-rackdc.properties
```
✅ You should see these values:

`dc=dc-seattle`<br>
`rack=rack-red`


This is the file that the *GossipingPropertyFileSnitch* uses to determine the rack and data center this particular node belongs to.

Racks and datacenters are purely logical assignments to Cassandra. You will want to ensure that your logical racks and data centers align with your physical failure zones.

Examine `cassandra-rackdc.properties` for *node2* and *node3*.

Properties for *node2* should be the same as for *node1*, they are in the same datacenter and on the same rack.

`dc=dc-seattle`<br>
`rack=rack-red`

Properties for *node3* should be different since it is in a different datacenter:

`dc=dc-atlanta`<br>
`rack=rack-green`

✅ Check on the cluster status:

<details class="katapod-details">
  <summary>Solution</summary>

```
nodetool status
```

</details>
<br>

You should now see that the nodes are in different datacenters.

<img src="https://katapod-file-store.s3.us-west-1.amazonaws.com/ds201/lab11-image01.png" />

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
  <a href='command:katapod.loadPage?[{"step":"step2"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>
