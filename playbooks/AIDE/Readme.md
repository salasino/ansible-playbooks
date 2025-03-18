# AIDE - Advanced Intrusion Detection Environment

Advanced Intrusion Detection Environment (AIDE) is an application that uses various tools to detect changes to particular files on a system and report on them so that you can maintain baseline file integrity and detect unauthorized changes and potential tootkits.
AIDE takes a "snapshot" of the state of the system, this "snapshot" is used to build a database. When an administrator wants to run an integrity test, AIDE compares the database against the current status of the system. Should a change have happened to the system between the snapshot creation and the test, AIDE will detect it and report it

# Playbooks

`installaide.yaml`:

The install and configure playbook will perform the following:
- Become the superuser.
- Check if the AIDE database exists. This is needed for idempotency, and will fail if the AIDE database exists.
- Install the AIDE package.
- Initialize AIDE, create a baseline, and enable the database.

`checkaide.yaml`:

The check playbook which runs on an Oracle Linux 8 host will perform the following:
- Become the superuser.
- Run the aide check command and report the result.
- If no differences are found, then report no differences and pass the job.
- If differences are found, then report differences and fail the job.

`aide_create_new_baseline.yaml`:

A new service requirement may need multiple hosts to have additional software installed and configured, following this installation and configuration any subsequent AIDE checks will fail. The create new baseline playbook will perform the following:
- Become the superuser.
- Run the initialize aide command.
- Re-enable the database.

`remove_aide.yaml`:

If it is necessary to remove the AIDE configuration from multiple hosts, then the remove aide playbook which runs on an Oracle Linux 8 host will perform the following:
- Become the superuser.
- Remove the AIDE package.
- Clean up the AIDE file system.

For more details on Advanced Intrusion Detection Environment with Oracle Linux Automation Manager, refer to the [Technical Paper](https://www.oracle.com/a/ocom/docs/linux/using-advanced-intrusion-detection-environment.pdf).
