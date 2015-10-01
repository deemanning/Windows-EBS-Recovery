# Windows-EBS-Recovery
EBS recovery procedures for Windows Servers (Restore-In-Place)

The following outlines the step-by-step process to execute an instance recovery of a Windows server with EBS snapshot volumes. This process aid in the test and evaluation of application upgrades, configuration changes, and all other server related changes that can potentially cause harm to the system. These instructions should be followed before changes are made to the server instance to ensure the continued operational status of a tenant application. This process does not require a launch of an ACB-Recovery-AMI. This process assumes that either schedule EBS snapshots are taken daily or a manual EBS snapshot of all volumes was completed prior to the recovery steps. This process also assumes that the administrator executing the recovery has adequate permissions to execute EBS snapshots, create volumes, attach volumes, and delete volumes.

Use Cases:

 - Full instance recovery
 - Configuration and Application testing

### The following should be completed before any critical changes are applied to the server instance:

Create a snapshot of each volume attached to the server instance

 - Name – Tag the name of the snapshot with an identical name of the server instance
 - Description – Note the purpose of the snapshot (Application Test, Configuration Test, etc... and the drive path “/dev/sda1”) “This make it easier to complete a filter search for the snapshots in the event there are several snapshots present and ensure that you know the drive path during the drive-attach configuration”

### Procedures 

1.Shutdown the server instance from the C2S console by executing “Stop”

2.Once the instance is completely stopped, create new EBS volumes from the snapshots that were previously created

 - Perform a filter search of the snapshot description (Application Test, etc...) “This will populate all the server instances that were affected by the change”
 - Select the Availability Zone from which the server is hosted for each new volume
 - After clicking “Create”, take note of the Volume IDs
 
3.Detach the current volumes from the broken server instance

4.Attach the snapshot volumes to the broken server instance

 - Complete a search for the Volume ID
 - Ensure that the Root drive is mounted as (/dev/sda1), all other drives depicted as (xvdf – xvdp)

5.Power on the instance and validate operational status

### Clean-Up process:

1.Delete the original EBS volumes that are no longer attached to the server instance

2.Delete the manually created snapshots

Note: The additional drives (D:, E:, etc...) that were attached to the instance prior to the recovery process may not automatically configure online once the server is powered on.

This only requires an administrator to manually configure the additional drives as “online” within Disk Management. However, by executing the “# Windows-Online-Disks" script on the server prior to any update or changes, all disks will automatically configure as online after a full instance recovery.
