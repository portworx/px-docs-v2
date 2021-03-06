# Upgrading with DC/OS

This guide walks through upgrading Portworx OCI container deployed on DCOS through the framework available in the DCOS catalog.

#### Update the Portworx image in the framework config {#update-the-portworx-image-in-the-framework-config}

The Portworx image to be used on each node is specified by the framework variable PORTWORX\_IMAGE\_NAME. To upgrade to a newer version you need to point this to the desired version. For example, if you want to upgrade to v1.2.11 you would set this to “portworx/px-enterprise:1.2.11”

![Portworx image option](https://docs.portworx.com/images/dcos-px-image-option.png)

#### Run the upgrade task {#run-the-upgrade-task}

Once the image name has been updated, the service file for Portworx needs to be updated on each node followed by a restart of the service. This can be done by running the `upgrade-portworx` plan. This will perform a rolling upgrade of Portworx so as not to cause an outage.

```text
dcos portworx plan start upgrade-portworx
{
  "message": "Received cmd: start"
}
```

Now wait for the upgrade tasks to go to COMPLETE state on all the agents

```text
dcos portworx plan status upgrade-portworx
upgrade-portworx (COMPLETE)
└─ upgrade (COMPLETE)
   ├─ portworx-0:[upgrade] (COMPLETE)
   ├─ portworx-1:[upgrade] (COMPLETE)
   ├─ portworx-2:[upgrade] (COMPLETE)
   ├─ portworx-3:[upgrade] (COMPLETE)
   └─ portworx-4:[upgrade] (COMPLETE)
```

At this point your Portworx cluster should be upgraded to the specified version.

