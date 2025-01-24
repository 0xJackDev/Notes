

Recovery Time object (RTO):
- This how long it takes to get up your systems up and running to a particular service level, it may be that your primary goal is to get a web server up and your RTO is how long it would take to get that web server up and running

Recovery Point objective (RPO):
- This is how much data needs to be available before we can say we are back up and running



Mean time to repair (MTTR):
- this is how long it takes to fix a issue



Mean time between failure (MTBF):
- this is a perdition of how long a device will be operational before a fail will occur






Network device backup and restore:
- every device has a configuration, this may be a IP address or security settings 
- You should have a process to automatically get the configuration of every machine and download it to a separate machine so we could back it up in case of failure
- Configurations are alot time specific to the version of firmware on a device its important to also have a backup of the current version of firmware 
- These backups are very helpful from when a piece of equipment comes in and we need a different configuration. WE can use backups to return to a previous version of the firmware then apply the configurations