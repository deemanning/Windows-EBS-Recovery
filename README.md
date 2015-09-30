# Windows-EBS-Recovery
EBS volume recovery procedures for Windows Servers
The following procedure outlines the step-by-step process that that must be followed to ensure a successful recovery of a Windows server.  This process assumes that either schedule EBS snapshots are taken daily or a manual EBS snapshot of all volumes was completed prior to the recovery steps.  This process also assumes that the administrator executing the recovery has adequate permissions to execute EBS snapshots, create volumes, attach volumes, and delete volumes.  

Use Cases:
- Full instance recovery
- Configuration and Application testing
